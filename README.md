# DesignPatterns

#Singleton

        class MySingleton{
            let adID = "ca-app-pub-1111111111111/444444"
            static let shareInstance = MySingleton()
            private init() {}
        }
        
explanation:
     
     static
makes 
     
     shareInstance
a class variable 
  
so you can do 
    
    let shared = MySingleton.shareInstance
    x = shared.adID
    
or

    MySingleton.shareInstance.adID
    
while     
    
    private init()

prevents you to do

        let x = MySingleton()
so you will not allow to create other instance/copy of this class (since it is a singleton)
