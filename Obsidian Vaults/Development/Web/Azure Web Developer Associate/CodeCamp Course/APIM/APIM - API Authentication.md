#azure #az-204 

In order to authenticate with our APIs, we configure those settings under the subscription section.
There is a **subscription required** checkbox.
- Checked: only developers with a valid access key can use it
- Unchecked: anyone can use it anonymously

Under the same section we can configure where the API will receive the access keys.
This can be set to either header or query string.

Under security, you're able to choose OAuth 2.0 or OpenID Connect.