# DesignPatterns

#Singleton

        class MySingleton{
            let adID = "ca-app-pub-1111111111111/444444"
            static let shareInstance = MySingleton()
            private init() {}
        }
        
explanation:

*static make "shareInstance" a class variable 
  
so you can do 
    let shared = MySingleton.shareInstance
    
    x = shared.adID
    
* private init()

this prevents you to let x = MySingleton()
prevent you to create other instance/copy of this class
