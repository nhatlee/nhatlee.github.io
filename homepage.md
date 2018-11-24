<header>
Things to Do
============
</header>
<main>
At Home
=======
*    Mow the cat
*    Feed the lawn

At the Office
=============
*    Learn Markdown
*    Use Big-O notation in a clever way
</main>
<!-- Document Title
==============

***24/Nov/2018***

**Post by:** *Nhat Le*

[create an anchor](#anchors-in-markdown)

# Head

## Item

### Detail (optional)

`some text`

`some text`

`some text`

For more information, see <http://www.example.com/>.

[ a link ](http://www.example.com/)

```
#!/bin/bash
echo Hello world
```

```bash
#!/bin/bash

echo Hello world
```

[
"JavaScript"
]

Some text

```swift
protocol ZPConnectorAPIProtocol {
    var delegate: ZPConnectorAPIOutputProtocol? {get set}
    func set(userInfo: ZPConnectorUserInfo)
    func recovery(start: UInt64, count: Int)
    func sendReadStatus(_ messageId: UInt64)
    func sendReceiveStatus(_ messageId: UInt64)
    func sendReceiveStatus(_ arrayMessageId: [UInt64])
    func sendDeleteStatus(_ messageId: UInt64)
    func ping(_ timeStamp: UInt64)
    func unsubcriber(completion:@escaping (Bool) -> Void)
    func startSubcriber(completion:@escaping (Bool) -> Void)
    func sendSubcriberRequest(completion:@escaping (Bool) -> Void)
    func request(requestId: UInt64, service: String, method: String, params: [String: String])
    func isConnected() -> Bool
    func closeConnection()
    func updateDeviceToken()
    func disconnect()
}
```

```
Another code block
```

Colons can be used to align columns.

| Tables        | Are           | Cool  |
| ------------- | :-----------: | ----: |
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      | $12   |
| zebra stripes | are neat      | $1    |

There must be at least 3 dashes separating each header cell.
The outer pipes (|) are optional, and you don't need to make the 
raw Markdown line up prettily. You can also use inline Markdown.

| Markdown | Less      | Pretty     |
| -------- | --------- | ---------- |
| *Still*  | `renders` | **nicely** |
| 1        | 2         | 3          |



<details> 
  <summary>Q1: What is the best Language in the World? </summary>
   A1: JavaScript 
</details>

```swift
func getCacheDataForAccountInfoInput() -> (String, String)? {
        guard self.interactor.isHaveCachedData() == true else { return nil }
        guard let headNumber = self.interactor.getCachedData(for: APIParamsKey.bankheadnumber.rawValue) as? String
            , let lastNumber = self.interactor.getCachedData(for: APIParamsKey.banklastnumber.rawValue) as? String else { return nil }
        return (headNumber, lastNumber)
    }
```
 -->
