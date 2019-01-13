---
title: Admin API – sourceDESK

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - php

toc_footers:
  - <a href='https://sourceway.de/en/imprint?layout=sourcedesk'>Imprint</a>

search: false
---

# Introduction

Welcome to the Admin API of sourceDESK. You can use this API as sourceDESK admin to access and manage objects in sourceDESK. Therefore, you need your API key, which you can create in the administration. This documentation covers all available API actions.

We provide example codes in Shell and PHP. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication & Request

> To make a request, use this code:

```php
<?php
$ch = curl_init("https://sourceway.de/admin/api.php/me");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  "Authorization: Bearer API_KEY",
]);
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://sourceway.de/admin/api.php/me" -H "Authorization: Bearer API_KEY"
```

> Make sure to replace `API_KEY` with your API key.

sourceDESK uses an API key to allow access to the API. You can find your API key in your admin area.

Parameters should be sent in the HTTP request body. The API is RESTful, it uses different HTTP methods like `GET` and `POST`.

sourceDESK expects for the API key to be included in all API requests to the server in the request.

A request URL is formatted as follows:

`/admin/api.php/ACTION`

<aside class="notice">
Hereby, <code>API_KEY</code> is your API key and <code>ACTION</code> is the task you want to execute.
</aside>

# Error handling

> An example error:

```json
{
  "error": "No action submitted."
}
```

If an error occures, the JSON response contains an element `error` with an error description. Make sure to watch out for errors and handle them.

# Admin

## Get my details

```php
<?php
$ch = curl_init("https://sourceway.de/admin/api.php/me");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  "Authorization: Bearer API_KEY",
]);
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://sourceway.de/admin/api.php/me" -H "Authorization: Bearer API_KEY"
```

> The above command returns JSON structured like this:

```json
{
  "username": "admin",
  "name": "John Doe",
  "email": "john.doe@example.com",
  "notes": "",
  "online": "0",
  "language": "english"
}
```

Using this endpoint, you can get details of your own admin account. This can be used to check successful authentication.

### HTTP request

`GET /me`

### Query Parameters

This request does not expect any parameters.

# Clients

## Get all clients

```php
<?php
$ch = curl_init("https://sourceway.de/admin/api.php/client");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  "Authorization: Bearer API_KEY",
]);
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://sourceway.de/admin/api.php/client" -H "Authorization: Bearer API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "ID": 1,
    "firstname": "John",
    "lastname": "Doe",
    "company": "",
    "mail": "john.doe@example.com"
  }
]
```

Using this endpoint, you can get a list of all clients.

### HTTP request

`GET /client`

### Query Parameters

This request does not expect any parameters.

## Get client details

```php
<?php
$ch = curl_init("https://sourceway.de/admin/api.php/client/1");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  "Authorization: Bearer API_KEY",
]);
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://sourceway.de/admin/api.php/client/1" -H "Authorization: Bearer API_KEY"
```

> The above command returns JSON structured like this:

```json
{
  "ID": 1,
  "mail": "john.doe@example.com",
  "salutation": "MALE",
  "firstname": "John",
  "lastname": "Doe",
  "name": "John Doe",
  "company": "",
  "vatid": "",
  "street": "Example street",
  "street_number": "1",
  "postcode": "12345",
  "city": "Example city",
  "country": 1,
  "country_alpha2": "US",
  "telephone": "",
  "fax": "",
  "birthday": "2019-01-13",
  "website": "",
  "language": "english",
  "currency": "USD",
  "credit": 200.00,
  "special_credit": 0.00,
  "registered": 1414250917,
  "last_login": 1536514408,
  "last_active": 1536514439,
  "last_ip": "8.8.8.8",
  "locked": false,
  "verified": true,
  "reseller": false,
  "login_notify": true,
  "newsletter": "3|2|1"
}
```

Using this endpoint, you can get the details of a client.

### HTTP request

`GET /client/CLIENT_ID`

<aside class="notice">Please replace <code>CLIENT_ID</code> with the customer ID of the client you want to get.</aside>

### Query Parameters

This request does not expect any parameters, except the client ID in the URL.

## Create a client

```php
<?php
$req = [
  "firstname" => "John",
  "lastname" => "Doe",
  "mail" => "john.doe@example.com",
];

$ch = curl_init("https://sourceway.de/admin/api.php/client");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  "Authorization: Bearer API_KEY",
]);
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://sourceway.de/admin/api.php/client" -H "Authorization: Bearer API_KEY" -X POST -d firstname=John -d lastname=Doe -d mail=john.doe@example.com
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "pwd": "XTuva2M7oBSK"
}
```

Using this endpoint, you can create a new client.

### HTTP request

`POST /client`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
firstname | - | **Required** Firstname of client
lastname | - | **Required** Lastname of client
mail | - | **Required** Email address of client
pwd | - | Password for client (if not set, a password is generated by system and returned)

## Modify a client

```php
<?php
$req = [
  "company" => "John Doe Ltd.",
];

$ch = curl_init("https://sourceway.de/admin/api.php/client/1");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  "Authorization: Bearer API_KEY",
]);
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://sourceway.de/admin/api.php/client/1" -H "Authorization: Bearer API_KEY" -X POST -d company=John+Doe+Ltd.
```

> The above command returns JSON structured like this:

```json
{
  "status": "ok"
}
```

Using this endpoint, you can modify an existing client.

### HTTP request

`PUT /client/CLIENT_ID`

<aside class="notice">Please replace <code>CLIENT_ID</code> with the customer ID of the client you want to modify.</aside>

### Query Parameters

You can use all columns of the database table `clients` as element containing the wished new value of this column. With one request, you can change as many values as you want.

# Invoices

## Get all invoices

```php
<?php
$ch = curl_init("https://sourceway.de/admin/api.php/invoice");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  "Authorization: Bearer API_KEY",
]);
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://sourceway.de/admin/api.php/invoice" -H "Authorization: Bearer API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "ID": 1,
    "client": 1,
    "date": "2019-01-13",
    "duedate": "2019-01-20",
    "customno": "",
    "status": "1",
  }
]
```

Using this endpoint, you can get a list of all invoices.

### HTTP request

`GET /invoice`

### Query Parameters

This request does not expect any parameters.

## Get invoice details

```php
<?php
$ch = curl_init("https://sourceway.de/admin/api.php/invoice/1");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  "Authorization: Bearer API_KEY",
]);
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://sourceway.de/admin/api.php/invoice/1" -H "Authorization: Bearer API_KEY"
```

> The above command returns JSON structured like this:

```json
{
  "ID": 1,
  "date": "2019-01-13",
  "duedate": "2019-01-20",
  "deliverydate": "2019-01-13",
  "client": 1,
  "customno": "",
  "status": 1,
  "reminder": 0,
  "no_reminders": false,
  "voucher": 0,
  "latefee": 0.00,
  "paid_amount": 0.00,
  "letter_sent": false,
  "encashment_provider": "",
  "encashment_file": "",
  "cancel_invoice": 0,
  "items": [
    {
      "ID": 1,
      "invoice": 1,
      "description": "Invoice position",
      "amount": 9.99,
      "relid": 0,
      "recurring": 0,
      "tax": true
    }
  ]
}
```

Using this endpoint, you can get the details of a client.

### HTTP request

`GET /invoice/INVOICE_ID`

<aside class="notice">Please replace <code>INVOICE_ID</code> with the invoice ID of the invoice you want to get.</aside>

### Query Parameters

This request does not expect any parameters, except the invoice ID in the URL.

## Create an invoice

```php
<?php
$req = [
  "client" => 1,
  "items" => [
    [
      "description" => "Invoice position",
      "amount" => 9.99,
      "tax" => true,
    ],
  ],
];

$ch = curl_init("https://sourceway.de/admin/api.php/client");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  "Authorization: Bearer API_KEY",
]);
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://sourceway.de/admin/api.php/client" -H "Authorization: Bearer API_KEY" -X POST --data "client=1&items%5B0%5D%5Bdescription%5D=Invoice+position&items%5B0%5D%5Bamount%5D=9.99&items%5B0%5D%5Btax%5D=1"
```

> The above command returns JSON structured like this:

```json
{
  "id": 1
}
```

Using this endpoint, you can create a new invoice.

### HTTP request

`POST /invoice`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
client | - | **Required** ID of customer
items[] | - | **At lease one is required** Array of items
- description | - | **Required** Description of invoice items
- amount | - | **Required** Amount of invoice items
- tax | false | Set to `true` if tax applies for item
date | - | Optional, otherwise todays date is used (Format: YYYY-MM-DD)
duedate | - | Optional, otherwise standard date is used (Format: YYYY-MM-DD)

## Modify an invoice

```php
<?php
$req = [
  "duedate" => "2019-01-27",
];

$ch = curl_init("https://sourceway.de/admin/api.php/invoice/1");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  "Authorization: Bearer API_KEY",
]);
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($req));
$res = curl_exec($ch);

if (curl_errno($ch)) {
  die(curl_error($ch));
}

curl_close($ch);
$res = json_decode($res, true);

print_r($res);
```

```shell
curl "https://sourceway.de/admin/api.php/invoice/1" -H "Authorization: Bearer API_KEY" -X POST -d date=2019-01-27
```

> The above command returns JSON structured like this:

```json
{
  "status": "ok"
}
```

Using this endpoint, you can modify an existing invoice.

### HTTP request

`PUT /invoice/INVOICE_ID`

<aside class="notice">Please replace <code>INVOICE_ID</code> with the customer ID of the invoice you want to modify.</aside>

### Query Parameters

You can use all columns of the database table `invoices` as element containing the wished new value of this column. With one request, you can change as many values as you want.

In addition, you can pass an `items` array to create new invoice items and modify existing ones. Each element of this array should also be an array with the following parameters:

Parameter | Default | Description
--------- | ------- | -----------
id | - | **Required for modification** Otherwise, new item is created
description | - | **Required** Description of invoice items
amount | - | **Required** Amount of invoice items
tax | false | Set to `true` if tax applies for item