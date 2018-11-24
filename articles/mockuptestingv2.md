<title>Document</title>
<div style="text-align: right"> 
***24/Nov/2018*** 
**Post by:** *Nhat Le*
</div>
# Add mockup testing in iOS project
###This post come from my experiences when develop new features for iOS app which need call request APIs but the server team still not develop those API yet, all things I have is just about the definitions of those API: host name, api paths, parameters, responses example.
###You cannot wait for server team deploy the real api then start your work, because you will missed the deadline. So I need to develop my features with dummy data response. But how to do that with out to change many code when the real api is ready? Bellow is my way to implement mockup testing:
###I decided to have a `struct` for setting the environments, like this:
```swift
           struct NetworkConfigEnvironment {
              let testing: Bool = false 
            }
```
