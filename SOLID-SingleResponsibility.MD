#each class should have one responsibility 

#I actually really like this all these class are basically functions

           class Handler {
              func handle() {
                  let data = request()
                  let array = parse(data: data)
                  save(array: array)
              }
              private func request() -> Data { }
              private func parse(data: Data) -> [String] { }
              private func save(array: [String]) { }
          }

//strange enough this does violate the principal it have 3 functions and private func can't bet unit tested.

          class Handler {
              let handler: Handler //instance of handler
              let parser: Parser //instance of Parser
              let dbHandler: DBHandler //instance of dbHandelr
              init(handler: Handler, parser: Parser, dbHandler: DBHandler) {
                  self.handler = handler
                  self.parser = parser
                  self.dbHandler = dbHandler
              }
              func handle() {
                  let data = handler.request()
                  let array = parser.parse(data: data)
                  dbHandler.save(array: array)
              }
          }

          class APIHandler { func request() -> Data {}}
          class ParseHandler { func parse(data: Data) -> [String] {} } 
          class DBHandler { func save(array: [String]) {} }

//now all these class can be tested

//all function can all be statics, in simple claases like this...is the same as..i guess making it a global function.

          class Handler {
              func handle() {
                  let data = APIHandler.request()
                  let array = ParseHandler.parse(data: data)
                  DBHandler.save(array: array)
              }
          }

          class APIHandler { static func request() -> Data {}}
          class ParseHandler { static func parse(data: Data) -> [String] {} } 
          class DBHandler { static func save(array: [String]) {} }


/***********************************************************************************************************/
example from: https://www.youtube.com/watch?v=gkxmeWvGEpU
/***********************************************************************************************************/

Not Solid: basically is the same problem as giant viewControllers You don't want things to get too big

      class Service {
          static func fetchProfileForUserID(userID: String) {}
      }
      class TimelineService {
          static func fetchTimelineForUserID(userID: String) {}  
      }
      class ServiceScheduler{ //ServiceScheduler(UserID:  , serviceTimer:    , timerTick:  )

          let userID: String
          private var serviceTimer: Timer?
          private var timerTick: Int
          init(userID: String) {
              self.userID = userID
              self.serviceTimer = nil
              self.timerTick = 0
          }
          func start() {
              serviceTimer = Timer.scheduledTimer(timeInterval: 1.0, target: self, selector: #selector(timerDidFire), userInfo: nil, repeats: true)
          }
          func stop() {
              serviceTimer?.invalidate()
              serviceTimer = nil
          }
          @objc private func timerDidFire(timer: Timer) {
              timerTick = timerTick + 1
              runServicesWithTick(tick: timerTick)
          }
          private func runServicesWithTick(tick: Int) {
              if ((tick % 1) == 0) { runTimelineUpdateService()}
              if ((tick % 2) == 0) { runProfileUpdateService()}
          }
          private func runTimelineUpdateService() { TimelineService.fetchTimelineForUserID(userID: userID)}
          private func runProfileUpdateService() { Service.fetchProfileForUserID(userID: userID) }
      }




 
