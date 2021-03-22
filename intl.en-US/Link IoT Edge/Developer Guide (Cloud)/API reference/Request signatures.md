# Request signatures

You must sign all API requests to ensure data security. Alibaba Cloud uses the request signature to verify the identity of the request sender. Therefore, each API request must contain signature information, regardless of whether it is sent through HTTP or HTTPS.

## Signature method

IoT Platform implements symmetric encryption with an AccessKey pair to verify the identity of the request sender. An AccessKey pair consists of an AccessKey ID and an AccessKey secret, which you can view in the [User Management console](https://usercenter.console.aliyun.com/#/manage/ak). The AccessKey ID is used to verify the identity of the user, while the AccessKey secret is used to encrypt and verify the signature string. You must keep your AccessKey secret strictly confidential.

**Note:** IoT Platform provides SDKs in multiple programming languages, such as Java, Python, and PHP. If you use these SDKs to call API operations, you can skip the signature process. For more information, see [Download IoT Platform SDKs](/intl.en-US/Developer Guide (Cloud)/SDK reference/Download IoT Platform SDKs.md) and related SDK documentation.

To sign a request, follow these steps:

1.  Create a canonicalized query string.

    1.  Arrange the request parameters.

        Arrange the request parameters \(including all [common](/intl.en-US/Developer Guide (Cloud)/API reference/Common parameters.md) and operation-specific parameters except Signature\) in alphabetical order.

        **Note:** If you use the GET method to send a request, the request parameters are included as a part of the request URL. The first parameter follows the question mark \(`?`\) in the URL, and the other parameters follow an ampersand \(`&`\).

    2.  Encode the canonicalized query string.

        Use UTF-8 to encode the names and values of the request parameters based on [RFC 3986](http://tools.ietf.org/html/rfc3986?spm=a2c4g.11186623.2.4.MQB3aI). Take note of the following encoding rules:

        -   Uppercase letters, lowercase letters, digits, and some special characters such as hyphens \(`-`\), underscores \(`_`\), periods \(`.`\), and tildes \(`~`\) do not need to be encoded.
        -   Other characters must be percent encoded in the `%XY` format. `XY` represents the ASCII code of the characters in hexadecimal notation. For example, double quotation marks \(`"`\) are encoded as `%22`.
        -   Extended UTF-8 characters are encoded in the `%XY%ZA…` format.
        -   Spaces must be encoded as `%20`. Do not encode spaces as plus signs \(`+`\).
        The preceding encoding method is similar to but slightly different from the `application/x-www-form-urlencoded` MIME encoding algorithm.

        If you use `java.net.URLEncoder` from the Java standard library, use `percentEncode` to encode request parameters and their values. In the encoded query string, replace the plus signs \(`+`\) with `%20`, asterisks \(`*`\) with `%2A`, and `%7E` with tildes \(`~`\). This way, you can obtain an encoded string that matches the preceding encoding rules.

        ```
        private static final String ENCODING = "UTF-8";
        private static String percentEncode(String value) throws UnsupportedEncodingException {
        return value ! = null ? URLEncoder.encode(value, ENCODING).replace("+", "%20").replace("*", "%2A").replace("%7E", "~") : null;
        }
        ```

    3.  Use an equal sign \(`=`\) to connect the name and value of each encoded request parameter.
    4.  Use an ampersand \(`&`\) to connect the encoded request parameters. These parameters must be arranged in the same order as those in Step a.
    Then, the canonicalized query string is created.

2.  Create a string-to-sign.

    Create a string-to-sign from the encoded canonicalized query string by using `percentEncode`. The following code provides an example on how to create a string-to-sign:

    ```
    StringToSign=
      HTTPMethod + "&" +                      // HTTPMethod: the HTTP method used to send the request, such as GET.
      percentEncode("/") + "&" +              // percentEncode("/"): Encode backslashes (/) as %2F.
      percentEncode(CanonicalizedQueryString) // Encode the canonicalized query string created in Step 1.
    ```

3.  Calculate the HMAC value of the string-to-sign by using the AccessKey secret as the key.

    Calculate the HMAC value of the string-to-sign based on [RFC 2104](https://www.ietf.org/rfc/rfc2104.txt). The Java Base64 encoding method is used in this example.

    ```
    Signature = Base64( HMAC-SHA1( AccessSecret, UTF-8-Encoding-Of(StringToSign) ) )
    ```

    **Note:** The AccessKey secret appended by an ampersand \(`&`\) \(ASCII code 38\) is used as the key for HMAC calculation. The SHA1 algorithm is used to calculate the HMAC value of the string-to-sign.

4.  Calculate the signature.

    Encode the HMAC value in Base64 to obtain the signature string.

5.  Add the signature.

    Add the signature string to the request as the Signature parameter and perform URL encoding based on [RFC 3986](http://tools.ietf.org/html/rfc3986).


## Examples

The following example demonstrates how to sign a request of calling the Pub operation. Assume that your AccessKey ID is `testid` and AccessKey secret is `testsecret`.

1.  Create and encode a canonicalized query string.

    ```
    http://iot.cn-shanghai.aliyuncs.com/?MessageContent=aGVsbG93b3JsZA%3D&Action=Pub&Timestamp=2017-10-02T09%3A39%3A41Z&SignatureVersion=1.0&ServiceCode=iot&Format=XML&Qos=0&SignatureNonce=0715a395-aedf-4a41-bab7-746b43d38d88&Version=2017-04-20&AccessKeyId=testid&SignatureMethod=HMAC-SHA1&RegionId=cn-shanghai&ProductKey=12345abcdeZ&TopicFullName=%2FproductKey%2Ftestdevice%2Fget
    ```

2.  Create a string-to-sign from the encoded canonicalized query string.

    ```
    GET&%2F&AccessKeyId%3Dtestid%26Action%3DPub%26Format%3DXML%26MessageContent%3DaGVsbG93b3JsZA%253D%26ProductKey%3D12345abcdeZ%26Qos%3D0%26RegionId%3Dcn-shanghai%26ServiceCode%3Diot%26SignatureMethod%3DHMAC-SHA1%26SignatureNonce%3D0715a395-aedf-4a41-bab7-746b43d38d88%26SignatureVersion%3D1.0%26Timestamp%3D2017-10-02T09%253A39%253A41Z%26TopicFullName%3D%252FproductKey%252Ftestdevice%252Fget%26Version%3D2017-04-20
    ```

3.  Calculate the signature.

    In this example, the AccessKey secret is `testsecret`. Therefore, the key used for HMAC calculation is testsecret&. The following code shows the calculated signature string:

    ```
    Y9eWn4nF8QPh3c4zAFkM/k/u7eA=
    ```

4.  Add the signature string to the request as the Signature parameter. The following code shows the URL of the signed request:

    ```
    http://iot.cn-shanghai.aliyuncs.com/?MessageContent=aGVsbG93b3JsZA%3D&Action=Pub&Timestamp=2017-10-02T09%3A39%3A41Z&SignatureVersion=1.0&ServiceCode=iot&Format=XML&Qos=0&SignatureNonce=0715a395-aedf-4a41-bab7-746b43d38d88&Version=2017-04-20&AccessKeyId=testid&Signature=Y9eWn4nF8QPh3c4zAFkM%2Fk%2Fu7eA%3D&SignatureMethod=HMAC-SHA1&RegionId=cn-shanghai&ProductKey=12345abcdeZ&TopicFullName=%2FproductKey%2Ftestdevice%2Fget
    ```


## Java code example

The following example demonstrates how to obtain a signature by using Java:

1.  Edit the Config.java file.

    ```
    /*   
     * Copyright © 2018 Alibaba. All rights reserved.
     */
    package com.aliyun.iot.demo.sign;
    
    /**
     * Signature configuration for the server API
     * 
     * @author: ali
     * @version: 0.1 2018-08-08 08:23:54
     */
    public class Config {
    
        // Your AccessKey pair.
        public static String accessKey = "1234567890123456";
        public static String accessKeySecret = "123456789012345678901234567890";
    
        public final static String CHARSET_UTF8 = "utf8";
    }
    ```

2.  Edit the UrlUtil.java file.

    ```
    /*   
     * Copyright © 2018 Alibaba. All rights reserved.
     */
    package com.aliyun.iot.demo.sign;
    
    import java.net.URLEncoder;
    import java.util.Map;
    
    import org.apache.commons.lang3.StringUtils;
    
    /**
     * URL processing class
     * 
     * @author: ali
     * @version: 0.1 2018-06-21 20:40:52
     */
    public class UrlUtil {
    
        private final static String CHARSET_UTF8 = "utf8";
    
        public static String urlEncode(String url) {
            if (! StringUtils.isEmpty(url)) {
                try {
                    url = URLEncoder.encode(url, "UTF-8");
                } catch (Exception e) {
                    System.out.println("Url encode error:" + e.getMessage());
                }
            }
            return url;
        }
    
        public static String generateQueryString(Map<String, String> params, boolean isEncodeKV) {
            StringBuilder canonicalizedQueryString = new StringBuilder();
            for (Map.Entry<String, String> entry : params.entrySet()) {
                if (isEncodeKV)
                    canonicalizedQueryString.append(percentEncode(entry.getKey())).append("=")
                            .append(percentEncode(entry.getValue())).append("&");
                else
                    canonicalizedQueryString.append(entry.getKey()).append("=").append(entry.getValue()).append("&");
            }
            if (canonicalizedQueryString.length() > 1) {
                canonicalizedQueryString.setLength(canonicalizedQueryString.length() - 1);
            }
            return canonicalizedQueryString.toString();
        }
    
        public static String percentEncode(String value) {
            try {
                // After you use URLEncoder.encode for encoding, replace plus signs (+), asterisks (*), and %7E with values that conform to the encoding standard specified by the API.
                return value == null ? null
                        : URLEncoder.encode(value, CHARSET_UTF8).replace("+", "%20").replace("*", "%2A").replace("%7E",
                                "~");
            } catch (Exception e) {
    
            }
            return "";
        }
    }
    ```

3.  Edit the SignatureUtils.java file.

    ```
    /*   
     * Copyright © 2018 Alibaba. All rights reserved.
     */
    package com.aliyun.iot.demo.sign;
    
    import java.io.IOException;
    import java.io.UnsupportedEncodingException;
    import java.net.URI;
    import java.net.URISyntaxException;
    import java.net.URLDecoder;
    import java.net.URLEncoder;
    import java.util.Map;
    import java.util.TreeMap;
    
    import javax.crypto.Mac;
    import javax.crypto.spec.SecretKeySpec;
    
    import org.apache.commons.codec.binary.Base64;
    import org.apache.commons.lang3.StringUtils;
    
    /**
     * Signature configuration for the server API
     * 
     * @author: ali
     * @version: 0.1 2018-06-21 20:47:05
     */
    public class SignatureUtils {
    
        private final static String CHARSET_UTF8 = "utf8";
        private final static String ALGORITHM = "HmacSHA1";
        private final static String SEPARATOR = "&";
    
        public static Map<String, String> splitQueryString(String url)
                throws URISyntaxException, UnsupportedEncodingException {
            URI uri = new URI(url);
            String query = uri.getQuery();
            final String[] pairs = query.split("&");
            TreeMap<String, String> queryMap = new TreeMap<String, String>();
            for (String pair : pairs) {
                final int idx = pair.indexOf("=");
                final String key = idx > 0 ? pair.substring(0, idx) : pair;
                if (! queryMap.containsKey(key)) {
                    queryMap.put(key, URLDecoder.decode(pair.substring(idx + 1), CHARSET_UTF8));
                }
            }
            return queryMap;
        }
    
        public static String generate(String method, Map<String, String> parameter, String accessKeySecret)
                throws Exception {
            String signString = generateSignString(method, parameter);
            System.out.println("signString---" + signString);
            byte[] signBytes = hmacSHA1Signature(accessKeySecret + "&", signString);
            String signature = newStringByBase64(signBytes);
            System.out.println("signature----" + signature);
            if ("POST".equals(method))
                return signature;
            return URLEncoder.encode(signature, "UTF-8");
        }
    
        public static String generateSignString(String httpMethod, Map<String, String> parameter) throws IOException {
            TreeMap<String, String> sortParameter = new TreeMap<String, String>();
            sortParameter.putAll(parameter);
            String canonicalizedQueryString = UrlUtil.generateQueryString(sortParameter, true);
            if (null == httpMethod) {
                throw new RuntimeException("httpMethod can not be empty");
            }
            StringBuilder stringToSign = new StringBuilder();
            stringToSign.append(httpMethod).append(SEPARATOR);
            stringToSign.append(percentEncode("/")).append(SEPARATOR);
            stringToSign.append(percentEncode(canonicalizedQueryString));
            return stringToSign.toString();
        }
    
        public static String percentEncode(String value) {
            try {
                return value == null ? null
                        : URLEncoder.encode(value, CHARSET_UTF8).replace("+", "%20").replace("*", "%2A").replace("%7E",
                                "~");
            } catch (Exception e) {
            }
            return "";
        }
    
        public static byte[] hmacSHA1Signature(String secret, String baseString) throws Exception {
            if (StringUtils.isEmpty(secret)) {
                throw new IOException("secret can not be empty");
            }
            if (StringUtils.isEmpty(baseString)) {
                return null;
            }
            Mac mac = Mac.getInstance("HmacSHA1");
            SecretKeySpec keySpec = new SecretKeySpec(secret.getBytes(CHARSET_UTF8), ALGORITHM);
            mac.init(keySpec);
            return mac.doFinal(baseString.getBytes(CHARSET_UTF8));
        }
    
        public static String newStringByBase64(byte[] bytes) throws UnsupportedEncodingException {
            if (bytes == null || bytes.length == 0) {
                return null;
            }
            return new String(Base64.encodeBase64(bytes, false), CHARSET_UTF8);
        }
    }
    ```

4.  Edit the Main.java file.

    ```
    /*   
     * Copyright © 2018 Alibaba. All rights reserved.
     */
    package com.aliyun.iot.demo.sign;
    
    import java.io.UnsupportedEncodingException;
    import java.net.URLEncoder;
    import java.util.HashMap;
    import java.util.Map;
    
    /**
     * Main entry to signature tools
     * 
     * @author: ali
     * @version: 0.1 2018-09-18 15:06:48
     */
    public class Main {
    
        // 1. Modify the AccessKey information in the Config.java file.
        // 2. You must specify all parameters. We recommend that you use Method 2 in the following description.
        // 3." The signature that follows Final signature is the signature that you want to obtain.
        public static void main(String[] args) throws UnsupportedEncodingException {
    
            // Method 1
            System.out.println("Method 1:");
            String str = "GET&%2F&AccessKeyId%3D" + Config.accessKey
                    + "%26Action%3DRegisterDevice%26DeviceName%3D1533023037%26Format%3DJSON%26ProductKey%3DaxxxUtgaRLB%26RegionId%3Dcn-shanghai%26SignatureMethod%3DHMAC-SHA1%26SignatureNonce%3D1533023037%26SignatureVersion%3D1.0%26Timestamp%3D2018-07-31T07%253A43%253A57Z%26Version%3D2018-01-20";
            byte[] signBytes;
            try {
                signBytes = SignatureUtils.hmacSHA1Signature(Config.accessKeySecret + "&", str.toString());
                String signature = SignatureUtils.newStringByBase64(signBytes);
                System.out.println("signString---" + str);
                System.out.println("signature----" + signature);
                System.out.println("Final signature:" + URLEncoder.encode(signature, Config.CHARSET_UTF8));
            } catch (Exception e) {
                e.printStackTrace();
            }
            System.out.println();
    
            // Method 2
            System.out.println("Method 2:");
            Map<String, String> map = new HashMap<String, String>();
            // The common parameters.
            map.put("Format", "JSON");
            map.put("Version", "2018-01-20");
            map.put("AccessKeyId", Config.accessKey);
            map.put("SignatureMethod", "HMAC-SHA1");
            map.put("Timestamp", "2018-07-31T07:43:57Z");
            map.put("SignatureVersion", "1.0");
            map.put("SignatureNonce", "1533023037");
            map.put("RegionId", "cn-shanghai");
            // The request parameters.
            map.put("Action", "RegisterDevice");
            map.put("DeviceName", "1533023037");
            map.put("ProductKey", "axxxUtgaRLB");
            try {
                String signature = SignatureUtils.generate("GET", map, Config.accessKeySecret);
                System.out.println("Final signature:" + signature);
            } catch (Exception e) {
                e.printStackTrace();
            }
            System.out.println();
        }
    }
    ```


