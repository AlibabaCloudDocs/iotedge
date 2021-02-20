# Signature

IoT Platform performs sender identity authentication for every access request. Therefore, you must include the signature information in requests, irrespective of the use of HTTP or HTTPS protocol.

## Signing method

**Note:** Alibaba Cloud provides SDKs in multiple programming languages, such as Java, Python, and PHP. If you use these SDKs, you can skip the signing process. See [Download SDKs](/intl.en-US/Developer Guide (Cloud)/SDK reference/Download SDKs.md).

When you are signing the parameters, you can view the AccessKey ID and the AccessKey Secret for your account on the [AccessKey](https://usercenter.console.aliyun.com/?spm=5176.2020520111.1001.d601.CMXhiF#/manage/ak) page in the console, and then encrypt them in symmetry. An AccessKey ID is used to identify the visitor, and an AccessKey Secret is the secret key used to encrypt the signature string and verify the signature string on the server. You must keep your AccessKey confidential to minimize the risk of data breaches.

Sign the request parameters as follows:

1.  Create a canonicalized query string.

    1.  Sort the request parameters in a lexicographical order.

        Sort the request parameters, including the [common request parameter](/intl.en-US/Developer Guide (Cloud)/API reference/Common parameters.md) \(except for Signature parameter\) and the special parameters of an interface in a lexicographical order.

        **Note:** When you make a request by using the GET method, these parameters constitute the part of the URL following `?` and are connected by `&`.

    2.  Encode the parameter names and values.

        Encode the request parameters by using the UTF-8 character set and according to the [RFC3986](http://tools.ietf.org/html/rfc3986?spm=a2c4g.11186623.2.4.MQB3aI) rules. The encoding rules are as follows:

        -   Do not encode A-Z, a-z , 0-9, and special characters including hyphens `-`, underscores `_`, periods `.` and tildes `~` .
        -   Encode other characters in the `%XY` format, with `XY` representing the hexadecimal ASCII value of the characters. For example, the half-width double quotes `"` are encoded as `%22`.
        -   Encode the extended UTF-8 characters in `%XY%ZA…` format.
        -   Encode whitespaces to `%20` instead of the plus signs `+`.
        Alternatively, you can use libraries that support the `application/x-www-form-urlencoded` MIME-type URL encoding.

        For example, you use `java.net.URLEncoder` of Java language. Firstly, use `percentEncode` to encode a string, and then replace plus signs `+` in the encoded string with `%20`, asterisks `*` with `%2A`, and `%7E` with tildes `~`. See the following example:

        ```
        private static final String ENCODING = "UTF-8";
        private static String percentEncode(String value) throws UnsupportedEncodingException {
        return value ! = null ? URLEncoder.encode(value, ENCODING).replace("+", "%20").replace("*", "%2A").replace("%7E", "~") : null;
        }
        ```

    3.  Connect the encoded parameter names and the values with equal signs `=`.
    4.  Connect all the request parameters with ampersands `&`. The order of the parameters must be the same as that in step a.
    You now have a canonicalized query string.

2.  Construct the string to be signed.

    You can use `percentEncode` to process the canonicalized query string that is created in step 1. See the following rules:

    ```
    StringToSign=
      HTTPMethod + "&" + //HTTPMethod: HTTP method used for making request, for example GET.
      percentEncode("/") + "&" + //percentEncode("/"): Encode backslash (/) to %2F.
      percentEncode(CanonicalizedQueryString) //Encode the canonicalized query string that is created in step 1.
    ```

3.  Calculate the HMAC value.

    Calculate the HMAC-SHA1 value of the `StringToSign` created in step 2, according to the [RFC2104](https://www.ietf.org/rfc/rfc2104.txt) rules. The Java Based64 encoding method is used in the following example:

    ```
    Signature = Base64( HMAC-SHA1( AccessSecret, UTF-8-Encoding-Of(StringToSign) ) )
    ```

    **Note:** When calculating for the signature value, you use the AccessKeySecret of your account and an ampersand `&` \(the hexadecimal ASCII value of an ampersand is 38\) as the key. The hash algorithm used is SHA1.

4.  Calculate the signature value.

    Encode the preceding HMAC value into a string based on Base64 encoding rules to obtain the signature value.

5.  Add the signature.

    Encode the Signature value according to the [RFC3986](http://tools.ietf.org/html/rfc3986) rules, and add the encoded signature value in the request.


## Signature example

Take calling the API Pub as an example, and suppose your AccessKey information is `AccessKeyId=testid`, and `AccessKeySecret=testsecret`.

1.  Create a canonicalized query string.

    ```
    http://iot.cn-shanghai.aliyuncs.com/?MessageContent=aGV***%3D&Action=Pub&Timestamp=2017-10-02T09%3A39%3A41Z&SignatureVersion=1.0&ServiceCode=iot&Format=XML&Qos=0&SignatureNonce=0715a39***&Version=2017-04-20&AccessKeyId=LTAI4***&SignatureMethod=HMAC-SHA1&RegionId=cn-shanghai&ProductKey=eZ***&TopicFullName=%2FproductKey%2Ftestdevice%2Fget
    ```

2.  Create a `StringToSign` based on the canonicalized query string.

    ```
    GET&%2F&AccessKeyId%3DLTAI4***%26Action%3DPub%26Format%3DXML%26MessageContent%3DaGV***A%253D%26ProductKey%3DeZ***%26Qos%3D0%26RegionId%3Dcn-shanghai%26ServiceCode%3Diot%26SignatureMethod%3DHMAC-SHA1%26SignatureNonce%3D0715a39***%26SignatureVersion%3D1.0%26Timestamp%3D2017-10-02T09%253A39%253A41Z%26TopicFullName%3D%252FproductKey%252Ftestdevice%252Fget%26Version%3D2017-04-20
    ```

3.  Calculate the HMAC-SHA1 value.

    Because you have the `AccessKeySecret=testsecret`, the key used in RFC2104 calculation is testsecret&. The HMAC-SHA1 value is:

    ```
    Y9eWn4nF8QPh3c4zAFkM/k/u7eA=
    ```

4.  Add this value to the request URL as the Signature parameter value to produce the following request URL:

    ```
    http://iot.cn-shanghai.aliyuncs.com/?MessageContent=aGV***%3D&Action=Pub&Timestamp=2017-10-02T09%3A39%3A41Z&SignatureVersion=1.0&ServiceCode=iot&Format=XML&Qos=0&SignatureNonce=0715a39***&Version=2017-04-20&AccessKeyId=LTAI4***&Signature=Y9eWn4nF8QPh3c4zAFkM%2Fk%2Fu7eA%3D&SignatureMethod=HMAC-SHA1&RegionId=cn-shanghai&ProductKey=eZ***&TopicFullName=%2FproductKey%2Ftestdevice%2Fget
    ```


## Java code sample

The following are examples of Java code for signing parameters:

1.  Config.java

    ```
    /*   
     * Copyright © 2018 Alibaba. All rights reserved.
     */
    package com.aliyun.iot.demo.sign;
    
    /**
     * API signature configuration file
     * 
     * @author: ali
     * @version: 0.1 2018-08-08 08:23:54
     */
    public class Config {
    
        // AccessKey information
        public static String accessKey = "1234567890123456";
        public static String accessKeySecret = "123456789012345678901234567890";
    
        public final static String CHARSET_UTF8 = "utf8";
    }
    ```

2.  UrlUtil.java

    ```
    /*   
     * Copyright © 2018 Alibaba. All rights reserved.
     */
    package com.aliyun.iot.demo.sign;
    
    import java.net.URLEncoder;
    import java.util.Map;
    
    import org.apache.commons.lang3. StringUtils;
    
    /**
     * URL encoding
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
                // After using URLEncoder.encode for encoding, replace"+","*", and "%7E" with values that conform to the encoding standard specified by the API
                return value == null ? null
                        : URLEncoder.encode(value, CHARSET_UTF8).replace("+", "%20").replace("*", "%2A").replace("%7E",
                                "~");
            } catch (Exception e) {
                
            }
            return "";
        }
    }
    ```

3.  SignatureUtils.java

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
    import org.apache.commons.lang3. StringUtils;
    
    /**
     * API signature
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

4.  Main.java

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
     * Main entry point of signature tool
     * 
     * @author: ali
     * @version: 0.1 2018-09-18 15:06:48
     */
    public class Main {
    
        // 1. Use the AccessKey information in Config.java.
        // 2. We recommend that you use Method 2 and you must provide all the parameters.
        // 3. The final signature is the value you need.
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
                System.out.println("signature: " + URLEncoder.encode(signature, Config.CHARSET_UTF8));
            } catch (Exception e) {
                e.printStackTrace();
            }
            System.out.println();
    
            // Method 2
            System.out.println("Method 2:");
            Map<String, String> map = new HashMap<String, String>();
            //Common parameters
            map.put("Format", "JSON");
            map.put("Version", "2018-01-20");
            map.put("AccessKeyId", Config.accessKey);
            map.put("SignatureMethod", "HMAC-SHA1");
            map.put("Timestamp", "2018-07-31T07:43:57Z");
            map.put("SignatureVersion", "1.0");
            map.put("SignatureNonce", "1533023037");
            map.put("RegionId", "cn-shanghai");
            // Request parameters
            map.put("Action", "RegisterDevice");
            map.put("DeviceName", "1533023037");
            map.put("ProductKey", "axxxUtgaRLB");
            try {
                String signature = SignatureUtils.generate("GET", map, Config.accessKeySecret);
                System.out.println("signature: " + signature);
            } catch (Exception e) {
                e.printStackTrace();
            }
            System.out.println();
        }
    }
    ```


