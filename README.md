# DesignPatterns

#Singleton

        class MySingleton{
            let adID = "ca-app-pub-1111111111111/444444"
            static let shareInstance = MySingleton()
            private init() {}
        }
  
  
example: saw something like this at work 
is used to store static information and states

Example 1

            class Manager{
            static let shared = Manager()

            private let viewShownKey = "viewShownKey"

            var viewShownBefore: Bool {
                get {
                    return UserDefaults.standard.bool(forKey: viewShownKey)
                }
                set {
                    UserDefaults.standard.set(newValue, forKey: viewShownKey)
                    UserDefaults.standard.synchronize()
                }
              }
            }

                print(Manager.shared.viewShownBefore) //false   if UserDefault bool return false when not found
                Manager.shared.viewShownBefore = true
                print(Manager.shared.viewShownBefore) // true
                Manager.shared.viewShownBefore = false
                print(Manager.shared.viewShownBefore)  //false
                
Example 2                
                
                enum Guide: String {
                    case x = "x map"
                    case y = "y map"
                }

                class GetStuffManager: NSObject {
                    static let sharedInstance = GetStuffManager()
                    func getGuide(name:String) -> [String] {

                        switch name {
                        case Guide.x.rawValue:
                            return ["1",
                                    "2",
                                    "3"]
                        case Guide.y.rawValue:
                            return ["a",
                                    "b",
                                    "c"
                                    ]
                        default:
                            return ["7",
                                    "8",
                                    "9",
                                    "10"]
                        }
                    }

                }

                GetStuffManager.sharedInstance.getGuide(name: "x map")  //1 2 3
                GetStuffManager.sharedInstance.getGuide(name: "y map") // a b c
                GetStuffManager.sharedInstance.getGuide(name: "asdf p") //7 8 9 10
                
                
 //example 3  (this is inside example 2)   
 //completion() is the caller can throw in bunch of code statements and make this function
 //execute them
 
               struct Vendor {
                    let name:String
                    let phone:String
                }
                class Manager: NSObject {

                    private var vendor = Vendor(name: "eric", phone: "1-888-1234")
                    static let shared = Manager()
                    public func updateContactInformation(completion: @escaping (() -> Void)){
                       //get vendor information from another class

                        //that class should have a function that fetch stuff
                        //and a completion handeler that give the information
                        //back to here
                        //info is some stuct that contain updated data
                            self.vendor = Vendor(name: info.name, phone: info.number )
                            completion()
                        }
                    }
                }

how to use this: In some class you can update the contract information and change your UI

                private var vendor: Vendor {
                     return Manager.shared.vendor
                }
                
                 Manager.shared.updateContactInformation(){
                          label.text = vendor.name 
                          //updateContractInformation updated the vendor struct inside Manger()
                          //we get vendor.name  vender fectch from  Manager()
                          //something like var vendor:Vendor { return defaultVendor}}
                 }
                        print("Updating vendor contact information after login")
                 }
                 
                 
