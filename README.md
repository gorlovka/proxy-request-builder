# Proxyrequest - parsing website - bypass cloudflare or any custom made protection

If you are looking for a way to parse website which is protected by cloudflare or some other custom made solution you are in the right place. 

Usually if you need to get a few dozens of pages from website you can go directry for webiste and scrape data easily.  Troubles comes if website has some kind of protection and you need to get a lot of data on regular basis.

We handle all blocking from protection on our behalf.
You get data like you were requesting them directly.

This solution is good if you need to get web pages, images and any other files not bigger than 30MB at most.
Not good if you need to download videos (not now, maybe in the future). 


Any javascript on requested page is not executed. You get the page as is. So if website enabled under protection mode this solution won't work.
This situation needs emulating browser which is resource taking and going to be expensive. Good news is that such delay for 5 seconds is not good for
users so if they use it they shoot themselves in the foot. If you need passing such protection, please contact me too. Just keep in mind that it's not passed by current solution you see.

## Usage via GET request

   Just do GET request  using any programming language or from browser:

    http://PROXY_SERVER_ADDRESS/api/forwardRequestInParallelV2?token=TOKEN_SECRET&urlToGet=urlEncodedInBase64
    
   That's all

   In response you get JSON object:

    {
	   "success":true,
	   "value":{
	      "statusCode":200,
	      "refererUsed":null,
	      "cookiesUsed":null,
	      "userAgentUsed":"Mozilla\/5.0 (Windows NT 6.2; WOW64; rv:42.0) Gecko\/20100101 Firefox\/42.0",
	      "content":"Field you are interested in",
	      "requestId" : "Id your query was assigned on server"
	   },
	   "message": "contains error description in the case of error",
	   "error":  false
	}

## There is a client for PHP

```
   // required parameter
    $proxyServerAddress= env('PROXY_SERVER');
    
    // required parameter
    $secretToken = env('TOKEN_SECRET');           
    
    // required parameter
    $urlToGet ='http://websiteProtectedFromParsing.com';    
    
    $proxyBuilder = new ProxyRequestBuilder($proxyServerAddress,
          $urlToGet, $secretToken, $isMobileOnlyBrowserHeaders ='0',
          $cookies =[], $referer ='');

    /**
     * Here you get raw content of requested page like
     *  you were requesting it directly
     */
    $content = $proxyBuilder->getContent();

    That's all
```


## Getting token
1. You can get **for FREE** token_secret which allows to handle up to **200** requests per day.
2.  More requests are supported on the premise of SaaS principles for paid subscription based count of request per month. Please contact me if you need more.

## Token specifics
Each token is valid of parsing only single wesbite. So please specify me its address in email.

## Contacts
Email for contacts is [jagen@meta.ua](mailto:jagen@meta.ua). I usually response with 12 hours or faster.  

Specify in email a) address of targeted webite, b) whether you would like to get free key or subscribe, c) desired approximate number of requests per day/month


## Russian 
Email для получения токена и адреса севера jagen@meta.ua.  

Поле $content содержит такое же содержимое, как если бы запрашивали напрямую

tokenApi - получение по запросу

userAgent - mobile_only - если нужно userAgent мобильного устройства,
поле какой именно заголовок был использован userAgentUsed возвращается в ответе


Использование:


        $proxyServerAddress= env('PROXY_SERVER');
        $secretToken = env('TOKEN_API_FOR_VIOLITY');
        $isMobileOnlyBrowserHeaders = '1'

        $cookies = [
           'a' => 5,
           'bbbb' => 7
        ];

        $referer = 'http://website.ua';

        $proxyBuilder = new ProxyRequestBuilder($proxyServerAddress,
              $urlToGet, $secretToken, $isMobileOnlyBrowserHeaders,
              $cookies, $referer);

        /**
         * Тут содержимое ответа
         */
        $content = $proxyBuilder->getContent();

        /**
         * Тут можно дополнительные поля получить
         */
        $cookies = $proxyBuilder->getCookiesUsed();
        $referer = $proxyBuilder->getRefererUsed();

        $userAgentUsed = $proxyBuilder->getUserAgentUsed();


        dump($userAgentUsed);

        dump($cookies);

        dump($referer);

        die('');

Поле $content содержит такое же содержимое, как если бы запрашивали напрямую

tokenApi - получение по запросу

userAgent - mobile_only - если нужно userAgent мобильного устройства,
поле какой именно заголовок был использован userAgentUsed возвращается в ответе
