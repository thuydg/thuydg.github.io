---
layout: blog
title: For Test
category: blog
tags: [php, coding, api]
summary: php coding to access api
image:
---

Use CI to test request to Nifty cloud mobile backend service.
Test request: push register request.


```
<?php
$message = 'Test Message';
$method = 'POST';
$fqdn   = 'mb.api.cloud.nifty.com';
$api_version = '2013-09-01';
$path        = 'push';
$timestamp = "2013-12-02T02:44:35.452Z";
$application_key = 'YOUR_APP_ID';
$client_key      = 'YOUR_CLIENT_ID';

$os = 'ios';

$header_string  = "SignatureMethod=HmacSHA256&";
$header_string .= "SignatureVersion=2&";
$header_string .= "X-NCMB-Application-Key=".$application_key . "&";
$header_string .= "X-NCMB-Timestamp=".$timestamp;

$signature_string  = $method . "\n";
$signature_string .= $fqdn . "\n";
$signature_string .= "/" . $api_version . "/" . $path ."\n";
$signature_string .= $header_string;

$signature = base64_encode(hash_hmac("sha256", $signature_string, $client_key, true));

$request = '
curl -v -X ' . $method . ' \
 -H "X-NCMB-Application-Key: ' . $application_key . '" \
 -H "X-NCMB-Timestamp: ' . $timestamp . '" \
 -H "X-NCMB-Signature: ' . $signature . '" \
 -H "Content-Type: application/json" -d \'{"immediateDeliveryFlag": true, "target":["' . $os . '"], "message":"' . $message . '","deliveryExpirationTime":"3 day"}\' \
 https://' . $fqdn . '/' . $api_version . '/push
';

$res = system($request);
print($request);

```
