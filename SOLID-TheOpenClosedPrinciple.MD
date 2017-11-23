        
        
        class Logger {
            func printData() {
                let cars = [ Car(name: "X", color: "R"), Car(name: "Y", color: "G"), Car(name: "Z", color: "Y")]
                cars.forEach { car in print(car.printDetails())}
            }
        }
        struct Car {
            let name: String
            let color: String
            func printDetails() -> String {
                return "I'm \(name) and my color is \(color)"
            }
        }
/* if you want to add to the class this is the bad way */

            class Logger {
                func printData() {
                    let cars = [ Car(name: "X", color: "B"),Car(name: "Y", color: "G"),Car(name: "Z", color: "Y")]
                    cars.forEach { car in print(car.printDetails())}
                    let bicycles = [ Bicycle(type: "A"), Bicycle(type: "B")]
                    bicycles.forEach { bicycles in print(bicycles.printDetails())}
                }
            }
            struct Car {
                let name: String
                let color: String
                func printDetails() -> String {return "I'm \(name) and my color is \(color)"}
            }
            struct Bicycle {
                let type: String
                func printDetails() -> String {
                    return "I'm a \(type)"
                }
            }
/* your suppose to do it this way according to the oopen close principal*/
what we have it that, you need to add a new loop just to print bikes
 
 actually i see how protocol can be useful it can be used as an type, so you can group similar things
 and put it in array insetad of any, and type cast it later


            protocol Printable { func printDetails() -> String}

            class Logger {
                func printData() {
                    var car:Car! //for testing
                    var bike: Bicycle!//for testing
                    
                    let vehicles: [Printable] = [
                        Car(name: "X", color: "a"),
                        Car(name: "Y", color: "b"),
                        Car(name: "Z", color: "c"),
                        Bicycle(type: "A"),
                        Bicycle(type: "B")
                    ]
                    vehicles.forEach { vehicle in
                        print(vehicle.printDetails())
                        
                        car = vehicles[0] as! Car //for testing
                        print(car) //for testing
                        bike = vehicles[3] as! Bicycle //for testing
                        print(bike) //for testing
                        car = vehicles[3] as! Bicycle //error - for testing
                        print(car) //error - for testing
                        
                        
                    }
                }
            }

            struct Car: Printable {
                let name: String
                let color: String
                func printDetails() -> String {
                    return "I'm \(name) and my color is \(color)"
                }
            }

            struct Bicycle: Printable {
                let type: String
                func printDetails() -> String {
                    return "I'm a \(type)"
                }
            }
         
