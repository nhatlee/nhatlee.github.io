# Setup mocking testing for iOS project

**_05_Nov_2018_**  
**Post by:** _Nhat Le_

This post come from my experiences when develop new features for iOS app which need call request APIs but the server team still not develop those API yet, all things I have is just about the definitions of those API: host name, api paths, parameters, responses example.

You cannot wait for server team deploy the real api then start your work, because you will missed the deadline. So I need to develop my features with dummy data response. But how to do that with out to change many code when the real api is ready? Bellow is my way to implement mockup testing:  
I decided to have a `struct` for setting the environments, like this:

```swift
 struct NetworkConfigEnvironment {
      let testing: Bool = false
}
```

And I will need a protocol to define my request apis method.EX:

```swift
protocol NetworkAPIProtocol {
    func checkOTP(from otp: String?) -> Observable&#60NetworkResponse&#62
}
```

The method `checkOTP` passing otp parameter and return an `Observable`(in rxSwift) for response result.  
Next step I need two struct one struct for implement real api call, and onether one handler return mockup json. Like bellow:

```swift
struct NetworkMockupAPI: NetworkAPIProtocol {
   //JSON is a typealias: JSON = [String: Any]
   private let responseStatus: [JSON]
   init(){
      var path = Bundle.main.path(forResource: "network_mockup", ofType: "json")
      responseStatus = loadNetworkMockup(path)
    }
   //Implement parser file json into method loadNetworkMockup
    func checkOTP(from otp: String?) -> Observable<NetworkResponse> {
       // return the Observable of mockup testing which fetch from network_mockup.json's file here
    }
}
```

### And below is the struct for real api:

```swift
struct NetworkRealAPI: NetworkAPIProtocol {
   func checkOTP(from otp: String?) -> Observable<NetworkResponse> {
    // Implement call real api here
   }
}
```

Finally you need an API router which will base on `NetworkConfigEnvironment` to decide for call mockup api or real api. Like that:

```swift
struct NetworkOTPInteractor {
   private var router: NetworkAPIProtocol
   init() {
      router = NetworkConfigEnvironment.testing ? NetworkMockupAPI() : NetworkRealAPI()
   }
   func checkOTP(from otp: String?) -> Observable<NetworkResponse> {
        return router.checkOTP(from: otp)
   }
}
```

That's it! You use `NetworkOTPInteractor` to call apis. And when need switching between mockup and real api just only change the `testing` variable.

### Done! :)
