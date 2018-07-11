# [kyototycoon](http://fallabs.com/kyototycoon/spex.html)

## What is Kyoto Tycoon?
Kyoto Tycoon (kt) is a lightweight database server.
For more detailed information please check the [official HP](http://fallabs.com/kyototycoon/spex.html).

## Kyoto Tycoon Docker Images

This is a Docker Image of Kyoto tycoon built on alpine.
Kyoto tycoon's lua extension is enabled.The version of each middle is below.

`alpine linux 3.8`  
`kyotocabinet 1.2.76`  
`kyototycoon 0.9.56`  
`lua 5.1.5-r4`

## How to use?

Start with the following command.

```:shell
docker run --name kyototycoon -p 1978:1978 -d kanga333/kyototycoon
```

Using HTTP Clients(Quoted from official HP.)

```:shell
# setting records
$ curl "http://localhost:1978/rpc/set?key=japan&value=tokyo"

# retrieving records
$ curl "http://localhost:1978/rpc/get?key=japan"
value   tokyo

# removing records
$ curl "http://localhost:1978/rpc/remove?key=japan"
```
