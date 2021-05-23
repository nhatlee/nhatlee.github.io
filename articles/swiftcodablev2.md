# Rough edges of Swift codable

11 Nov 2018
**Post by:** _Nhat Le_

Swift codable help auto-generated json to your object models more easily.  
To see how it work, just suppose we have a login api which will response the user info as the json:

```json
{
  "userid": 1002,
  "user_name": "nhatle",
  "email": "lenhathk@gmail.com",
  "access_token": "akjfkadT10cm543sfdsf"
}
```

How to parse the json to your user model?. It's really easy, first of all you need define your user model like that:

```swift
struct UserModel: Codable {
   let id: Int
   let name: String
   let email: String
   let token: String
   enum CodingKeys: String, CodingKey {
        case id = "userid"
        case name = "user_name"
        case email
        case token = "access_token"
  }
}
```

As you see the field `email` in CodingKeys enum didn't have string to represent for it, just because the field name have same string with the key in json string. Now, you parse the json string to your model like that:

```swift
do {
    let jsonData = json.data(using: .utf8)!
    let user = try JSONDecoder().decode(UserModel.self, from: jsonData)
    }
catch let error {
    print(error.localizedDescription)
}
```

How about nested json? like that:

```json
{
  "userid": 1002,
  "user_name": "nhatle",
  "email": "lenhathk@gmail.com",
  "access_token": "akjfkadT10cm543sfdsf",
  "addresses": [
    {
      "street": "Linh Dong",
      "city": "HO CHI MINH"
    },
    {
      "street": "Thanh Thai",
      "city": "HO CHI MINH"
    }
  ]
}
```

Don't worry, you just need to change a little bit your user model and add `Address` model to make your code run properly:

```swift
struct UserModel: Codable {
  let id: Int
  let name: String
  let email: String
  let token: String
  let addresses: [Address]
  enum CodingKeys: String, CodingKey {
     case id = "userid"
     case name = "user_name"
     case email
     case token = "access_token"
    case addresses
   }
}
struct Address: Codable {
   let street: String
   let city: String
}
```

You done, with out need change any code in the place you parsed the json to your model as above.  
All things seem run smoothly until the day server team decided that into the response json of the login api `addresses`'s field is optional. It's mean some users will have addresses field and another will miss it. And the the code you did before not run for some users which don't have addresses.  
You can change the codable model to fixed it by adding `required init(from decoder: Decoder) throws` to your user model:

```swift
required init(from decoder: Decoder) throws {
    let container = try decoder.container(keyedBy: CodingKeys.self)
    self.name = try container.decodeIfPresent(String.self, forKey: .name) ?? "Your default value"
       ...
    self.addresses = try container.decodeIfPresent(Array<Address>.self, forKey: .addresses) ?? []
}
```

Done! But it's still ridiculous that auto-generated methods cannot read the default values from optionals.
