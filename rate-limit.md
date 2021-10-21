# Requirement
> What's the scale of system?

It should be a large system can handle 10k user

> Is system work in distributed environment?

Of course not

> Where to implement rate limit?

I prefer server side, cause client side exposed logic outside, that may have some security issue.

So there are 3 kind of approach to implement rate limit in server side:
1. load balancer / api gateway
2. web server / api server
3. router

I gonna choose web server and make a middleware to be a rate limiter

> How many user can access system in the same time? the max request volume?

I hope the system can handle 10k user in the same time and the basic request per second could be 3

> Which property is a identifier for rate limiter to recognize request?

I hope identifier can be fiexible, so up to you young man

> Where is client request send from?

Client could send request from Web or Mobile

# Strategy
- Principle
  - Low latency
  - Accurately limit request
  - No rate limiting
  - Exception handler
- Limit scope
  - User Role
  - Specific HTTP endpoint
- Identifier
  - IP address & user token
- Algorithm
  - Token bucket
- Where to implement
  - Server side
# High level design

![](https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1&title=Rate%20limiting#R7ZlLc9owEMc%2FDccwlm35cUyA0nSSNimdSTh1hC2wJsZiZPHqp6%2BM5YcQnRACUQ7lgrWS1tZv%2F16t7Y7Tm2%2BGDC2SexrjtGNb8abj9Du2DdzAEX%2BFZVta%2FACUhhkjsRzUGEbkD5ZGS1qXJMa5MpBTmnKyUI0RzTIcccWGGKNrddiUpupZF2iGNcMoQqlufSIxT0prYPuN%2FSsms6Q6M%2FDCsmeOqsFyJXmCYrpumZxBx%2BkxSnl5NN%2F0cFrAq7iU8778o7e%2BMIYzfswE1Iejx%2Fl4eTt2psMfvx6T3%2FfWlYzOCqVLuWB5sXxbEWB0mcW4cGJ1nJt1QjgeLVBU9K5FzIUt4fNUtIA4nJI07dGUst1cJ0Y4mEbCHqM82fkoBuWc0RfcGuZFAZ5MRY%2B%2BJrnMFWYcb1omucYhpnPM2VYMqXqh5C0FZ%2FuyvW7CBwNpS1qhcysjkpKZ1b4bquJAgn0DZFuDfEdRLCw3KEVZhFnH9tC8IJlN8kWN4dQYnAGiA%2FYgAh2iDQ9ABNalILoaxD7iaIJybJ6Wp9LyoE4L2AdoeZeCBTVYT4ObAhJmq0JunwwYtE0D8zRgPxEXyrJSMiecZLMio5M4TvFaLNw8QFcF6BxIcsD7SIC%2BBrCHosQ8qTrVS1KucakFOqmUFAs0jcqBjoIqNE0q1En1vxvH5FvGKK2H%2FGrQEyU2ubt%2B%2BBYH2ehqdqC60BDhLL4uamHRilKU5yRSqagIBRq2fZZdu8a46OnCqtnftEf2t3Wrqt%2B9usirama3Zo9jreDWgsERm2H%2BmjL0CLVLvAMhqGwMp4iTlXoZh%2BIiz%2FBASXF7NveJqoA63JWLnC5ZhOWsdkW%2B78jac%2BTsOSo5aI52MqmXfbpy9JLqXMqxui4IVfVYlv1O%2FeAN4c%2BNEkVrXIlUHDdOi8a2fYYHzIhghZk0Hi%2FEMpKvJ%2FNXBWt%2FKsHu56JjBQvCVxxdWLB6lfZfsG3BmhKYYNcFavFQP0G%2BVWOiQOsGgerLt7q21frBD1WdXtqeTXXn3WArvYGW2hrtHdbbGXOhd2Qu9E1KFYLizm5%2BQFGau78DH6taCEDXd8Pmp7oNjQpYf%2BI4X9qEioQNJEwDAoZmc%2B3eA%2B2pknX3NnPt%2FeeFVak%2F3b1blebUZXLnhepuCf2wG4ZaKjphH1bc1i81P0gelcxb%2BrjNREmUoWJqhvmashdNMe%2F5WDENIhxFh75PTALowkYO2ruCowTxhu8T53qBIJrN96UyMM1XOmfwFw%3D%3D)

# Bonus: Network layer implement rate limit

https://content.cisco.com/chapter.sjs?uri=%2Fsearchable%2Fchapter%2Fcontent%2Fen%2Fus%2Ftd%2Fdocs%2Fios-xml%2Fios%2Fipv6_basic%2Fconfiguration%2Fxe-16-9%2Fip6b-xe-16-9-book%2Fip6-icmp-rate-lmt-xe.html.xml&platform=Cisco%204000%20Series%20Integrated%20Services%20Routers&release=IOS%20XE%20Fuji%2016.9.x#GUID-904DCAFD-2FDB-4596-A549-086EC9023648

# Bonus: Application layer - load balancer implement rate limit