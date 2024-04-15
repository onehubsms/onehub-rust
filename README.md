# Onehub Rust Library
```Rust
extern crate reqwest;
use reqwest::header;

fn main() -> Result<(), Box> {
    let mut headers = header::HeaderMap::new();
    headers.insert("Content-Type", "application/json".parse().unwrap());
    headers.insert("x-api-user", "API_USERNAME_HERE".parse().unwrap());
    headers.insert("x-api-key", "API_KEY_HERE".parse().unwrap());

    let client = reqwest::blocking::Client::builder()
        .redirect(reqwest::redirect::Policy::none())
        .build()
        .unwrap();
    let res = client.post("https://api.onehub.co.ke/v1/sms/send")
        .headers(headers)
        .body("{\"phoneNumbers\": \"+2547XXXXXXXX,+2547XXXXXXXX\", \"message\": \"Hello Api!\",\"senderId\":\"Onehub\"}")
        .send()?
        .text()?;
    println!("{}", res);

    Ok(())
}
```
# Username and API Key
You can get your username and API Key [here](https://dashboard.onehub.co.ke/account/0/user/signup).
# Request Body Parameters
`phoneNumbers` - `[Type: String]` `[Required]` - Phone numbers of the recipients in international format with the plus (+) sign. Multiple numbers should be comma-separated.

`Message` - `[Type: String]` `[Required]` - The message you want to send. Each message is counted as 160 characters long. Messages longer than 160 characters will be billed accordingly.

`Sender ID` - `[Type: String]` `[Required]` - A sender ID serves as a branding for outgoing messages, typically representing your company name. Your users will receive messages with your specified sender ID. You can apply for your sender ID on our [website](https://onehub.co.ke/).
