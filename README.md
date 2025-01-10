# Documentación Nequi

Documentación de la integración de Fleteo con Nequi para pagos en línea.

---

## Índice

1. [Solicitud para obtener Token de Nequi](#1-solicitud-para-obtener-token-de-nequi)
2. [Pagos exitosos](#2-pagos-exitosos)
3. [Pagos rechazados](#3-pagos-rechazados-desde-la-app)

---

## 1. Solicitud para obtener Token de Nequi

  ### URL

  `https://oauth.sandbox.nequi.com/oauth2/token?grant_type=client_credentials`

  ### Cuerpo de la solicitud

  ```json
  {
    "access_token": "eyJraWQiOiJuZVhiaFBIVkREV3IxXC9sZTl2YVdVQ0laNHlrSHZsUkF0bjFGajBRSVU3WT0iLCJhbGciOiJSUzI1NiJ9..."
  }
  ```

  ### Respuesta obtenida

  - **Acess Token**: (*token*)

---

## 2. Pagos exitosos

- ### **Solicitud de notificación push**

  ### URL

  `https://api.sandbox.nequi.com/payments/v2/-services-paymentservice-unregisteredpayment`

  ### Cuerpo de la solicitud

  ```json
  {
    "RequestMessage": {
      "RequestHeader": {
        "Channel": "PNP04-C001",
        "RequestDate": "2025-01-10T15:17:38Z",
        "MessageID": "29e9f412-7ae8-4377-8052-ef220ff98e38",
        "ClientID": "12345",
        "Destination": {
          "ServiceName": "PaymentsService",
          "ServiceOperation": "unregisteredPayment",
          "ServiceRegion": "C001",
          "ServiceVersion": "1.0.0"
        }
      },
      "RequestBody": {
        "any": {
          "unregisteredPaymentRQ": {
            "phoneNumber": "3560567253",
            "code": "NIT_1",
            "value": "4165",
            "reference1": "reference1",
            "reference2": "reference2",
            "reference3": "reference3"
          }
        }
      }
    }
  }
  ```

  ### Respuesta obtenida

  - **Cuerpo de la respuesta**:

    ```json
    {
      "ResponseMessage": {
        "ResponseHeader": {
          "Channel": "PNP04-C001",
          "ResponseDate": "2025-01-10T15:17:49.747Z",
          "Status": {
            "StatusCode": "0",
            "StatusDesc": "SUCCESS"
          },
          "MessageID": "29e9f412-7ae8-4377-8052-ef220ff98e38",
          "ClientID": "12345",
          "Destination": {
            "ServiceName": "PaymentsService",
            "ServiceOperation": "unregisteredPayment",
            "ServiceRegion": "C001",
            "ServiceVersion": "1.0.0"
          }
        },
        "ResponseBody": {
          "any": {
            "unregisteredPaymentRS": {
              "transactionId": "350-12345-36517011-29e9f412-7ae8-4377-8052-ef220ff"
            }
          }
        }
      }
    }
    ```

  - **ID de Transacción**: `350-12345-36517011-29e9f412-7ae8-4377-8052-ef220ff`
  
- ### **Consultando Estado del Pago**

  ### URL

  `https://api.sandbox.nequi.com/payments/v2/-services-paymentservice-getstatuspayment`

  ### Cuerpo de la solicitud

  ```json
  {
    "RequestMessage": {
      "RequestHeader": {
        "Channel": "PNP04-C001",
        "RequestDate": "2025-01-10T15:20:52Z",
        "MessageID": "e6935dd7-2624-4f4e-82da-4d5afc9a7066",
        "ClientID": "12345",
        "Destination": {
          "ServiceName": "PaymentsService",
          "ServiceOperation": "getStatusPayment",
          "ServiceRegion": "C001",
          "ServiceVersion": "1.0.0"
        }
      },
      "RequestBody": {
        "any": {
          "getStatusPaymentRQ": {
            "codeQR": "350-12345-36517011-29e9f412-7ae8-4377-8052-ef220ff"
          }
        }
      }
    }
  }
  ```

  ### Respuesta obtenida

  - **Cuerpo de la respueta**:

    ```json
    {
      "ResponseMessage": {
        "ResponseHeader": {
          "Channel": "PNP04-C001",
          "ResponseDate": "2025-01-10T15:20:56.961Z",
          "Status": {
            "StatusCode": "0",
            "StatusDesc": "SUCCESS"
          },
          "MessageID": "e6935dd7-2624-4f4e-82da-4d5afc9a7066",
          "ClientID": "12345",
          "Destination": {
            "ServiceName": "PaymentsService",
            "ServiceOperation": "getStatusPayment",
            "ServiceRegion": "C001",
            "ServiceVersion": "1.0.0"
          }
        },
        "ResponseBody": {
          "any": {
            "getStatusPaymentRS": {
              "date": "2025-01-10 10:17:41",
              "trnId": "12345",
              "phoneNumber": "3560567253",
              "originMoney": [{}],
              "name": "EL RANCHERO1",
              "ipAddress": "N/A",
              "value": "4165",
              "status": "35"
            }
          }
        }
      }
    }
    ```

  - **Estado del Pago**: `35`

---

## 3. Pagos rechazados desde la app

- ### **Solicitud de notificación push**

  ### URL

  `https://api.sandbox.nequi.com/payments/v2/-services-paymentservice-unregisteredpayment`

  ### Cuerpo de la solicitud

  ```json
  {
    "RequestMessage": {
      "RequestHeader": {
        "Channel": "PNP04-C001",
        "RequestDate": "2025-01-10T19:16:09Z",
        "MessageID": "37d53ecf-9f26-4552-b224-9ff36c1faefa",
        "ClientID": "12345",
        "Destination": {
          "ServiceName": "PaymentsService",
          "ServiceOperation": "unregisteredPayment",
          "ServiceRegion": "C001",
          "ServiceVersion": "1.0.0"
        }
      },
      "RequestBody": {
        "any": {
          "unregisteredPaymentRQ": {
            "phoneNumber": "3560567253",
            "code": "NIT_1",
            "value": "4165",
            "reference1": "reference1",
            "reference2": "reference2",
            "reference3": "reference3"
          }
        }
      }
    }
  }
  ```

  ### Respuesta obtenida

  - **Cuerpo de la respuesta**:

    ```json
    {
     "ResponseMessage": {
       "ResponseHeader": {
         "Channel": "PNP04-C001",
         "ResponseDate": "2025-01-10T19:16:21.266Z",
         "Status": {
           "StatusCode": "0",
           "StatusDesc": "SUCCESS"
         },
         "MessageID": "37d53ecf-9f26-4552-b224-9ff36c1faefa",
         "ClientID": "12345",
         "Destination": {
           "ServiceName": "PaymentsService",
           "ServiceOperation": "unregisteredPayment",
           "ServiceRegion": "C001",
           "ServiceVersion": "1.0.0"
         }
       },
       "ResponseBody": {
         "any": {
           "unregisteredPaymentRS": {
             "transactionId": "350-12345-36517011-37d53ecf-9f26-4552-b224-9ff36c1"
           }
         }
       }
      }
    }
    ```

  - **ID de Transacción**: `350-12345-36517011-37d53ecf-9f26-4552-b224-9ff36c1`

- ### **Consultando Estado del Pago**

  ### URL

  `https://api.sandbox.nequi.com/payments/v2/-services-paymentservice-getstatuspayment`

  ### Cuerpo de la solicitud

  ```json
  {
    "RequestMessage":{
      "RequestHeader":{
        "Channel":"PNP04-C001",
        "RequestDate":"2025-01-10T19:19:23Z",
        "MessageID":"8ae67293-602d-4cf7-9e7b-bd2fee35060c",
        "ClientID":"12345",
        "Destination":{
          "ServiceName":"PaymentsService",
          "ServiceOperation":"getStatusPayment",
          "ServiceRegion":"C001",
          "ServiceVersion":"1.0.0"
        }
      },
      "RequestBody":{
        "any":{
          "getStatusPaymentRQ":{
            "codeQR":"350-12345-36517011-37d53ecf-9f26-4552-b224-9ff36c1"
          }
        }
      }
    }
  }
  ```

  ### Respuesta obtenida

  - **Cuerpo de la respueta**:

    ```json
    {
      "ResponseMessage":{
        "ResponseHeader":{
          "Channel":"PNP04-C001",
          "ResponseDate":"2025-01-10T19:19:24.101Z",
          "Status":{
            "StatusCode":"10-455",
            "StatusDesc":"La transacción esta cancelada"
          },
          "MessageID":"8ae67293-602d-4cf7-9e7b-bd2fee35060c",
          "ClientID":"12345",
          "Destination":{
            "ServiceName":"PaymentsService",
            "ServiceOperation":"getStatusPayment",
            "ServiceRegion":"C001",
            "ServiceVersion":"1.0.0"
          }
        },
        "ResponseBody":{
          "any":{

          }
        }
      }
    }
    ```

  - **Estado del Pago**: `10-455`

---
