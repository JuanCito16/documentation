# Documentación Nequi

Documentación de la integración de Fleteo con Nequi para pagos en línea.

---

## Índice

1. [Solicitud para obtener Token de Nequi](#1-solicitud-para-obtener-token-de-nequi)
2. [Pagos exitosos](#2-pagos-exitosos)
3. [Pagos rechazados](#3-pagos-rechazados-desde-la-app)
4. [Pagos expirados](#4-pagos-expirados)
5. [Pagos con numeros no vinculados](#5-pagos-con-número-que-no-tiene-cuenta-nequi)
6. [Servicio de reverso](#6-uso-del-servicio-de-reverso-de-pagos)
7. [Experiencia de usuario](#7-experiencia-de-usuario)

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
    "RequestMessage":{
      "RequestHeader":{
        "Channel":"PNP04-C001",
        "RequestDate":"2025-01-17T21:12:54Z",
        "MessageID":"MqYjk3O2UP",
        "ClientID":"12345",
        "Destination":{
          "ServiceName":"PaymentsService",
          "ServiceOperation":"unregisteredPayment",
          "ServiceRegion":"C001",
          "ServiceVersion":"1.0.0"
        }
      },
      "RequestBody":{
        "any":{
          "unregisteredPaymentRQ":{
            "phoneNumber":"3560567253",
            "code":"NIT_1",
            "value":"5950",
            "reference1":"reference1",
            "reference2":"reference2",
            "reference3":"reference3"
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
      "ResponseMessage":{
        "ResponseHeader":{
          "Channel":"PNP04-C001",
          "ResponseDate":"2025-01-17T21:13:05.522Z",
          "Status":{
            "StatusCode":"0",
            "StatusDesc":"SUCCESS"
          },
          "MessageID":"MqYjk3O2UP",
          "ClientID":"12345",
          "Destination":{
            "ServiceName":"PaymentsService",
            "ServiceOperation":"unregisteredPayment",
            "ServiceRegion":"C001",
            "ServiceVersion":"1.0.0"
          }
        },
        "ResponseBody":{
          "any":{
            "unregisteredPaymentRS":{
              "transactionId":"350-12345-36517011-MqYjk3O2UP"
            }
          }
        }
      }
    }
    ```

  - **ID de Transacción**: `350-12345-36517011-MqYjk3O2UP`
  
- ### **Consultando Estado del Pago**

  ### URL

  `https://api.sandbox.nequi.com/payments/v2/-services-paymentservice-getstatuspayment`

  ### Cuerpo de la solicitud

  ```json
  {
    "RequestMessage":{
      "RequestHeader":{
        "Channel":"PNP04-C001",
        "RequestDate":"2025-01-17T21:16:07Z",
        "MessageID":"vFjkFY7s4Z",
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
            "codeQR":"350-12345-36517011-MqYjk3O2UP"
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
          "ResponseDate":"2025-01-17T21:16:12.647Z",
          "Status":{
            "StatusCode":"0",
            "StatusDesc":"SUCCESS"
          },
          "MessageID":"vFjkFY7s4Z",
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
            "getStatusPaymentRS":{
              "date":"2025-01-17 16:12:57",
              "trnId":"12345",
              "phoneNumber":"3560567253",
              "originMoney":[
                {
                  
                }
              ],
              "name":"EL RANCHERO1",
              "ipAddress":"N/A",
              "value":"5950",
              "status":"35"
            }
          }
        }
      }
    }
    ```

  - **Estado del Pago**: `35`

  - **Comprobante**:
    ![comprobante](images/comprobante.jpeg)

---

## 3. Pagos rechazados desde la app

- ### **Solicitud de notificación push**

  ### URL

  `https://api.sandbox.nequi.com/payments/v2/-services-paymentservice-unregisteredpayment`

  ### Cuerpo de la solicitud

  ```json
  {
    "RequestMessage":{
      "RequestHeader":{
        "Channel":"PNP04-C001",
        "RequestDate":"2025-01-20T14:24:50Z",
        "MessageID":"KDcyo8JTLc",
        "ClientID":"12345",
        "Destination":{
          "ServiceName":"PaymentsService",
          "ServiceOperation":"unregisteredPayment",
          "ServiceRegion":"C001",
          "ServiceVersion":"1.0.0"
        }
      },
      "RequestBody":{
        "any":{
          "unregisteredPaymentRQ":{
            "phoneNumber":"3560567253",
            "code":"NIT_1",
            "value":"5950",
            "reference1":"reference1",
            "reference2":"reference2",
            "reference3":"reference3"
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
      "ResponseMessage":{
        "ResponseHeader":{
          "Channel":"PNP04-C001",
          "ResponseDate":"2025-01-20T14:25:02.997Z",
          "Status":{
            "StatusCode":"0",
            "StatusDesc":"SUCCESS"
          },
          "MessageID":"KDcyo8JTLc",
          "ClientID":"12345",
          "Destination":{
            "ServiceName":"PaymentsService",
            "ServiceOperation":"unregisteredPayment",
            "ServiceRegion":"C001",
            "ServiceVersion":"1.0.0"
          }
        },
        "ResponseBody":{
          "any":{
            "unregisteredPaymentRS":{
              "transactionId":"350-12345-36517011-KDcyo8JTLc"
            }
          }
        }
      }
    }
    ```

  - **ID de Transacción**: `350-12345-36517011-KDcyo8JTLc`

- ### **Consultando Estado del Pago**

  ### URL

  `https://api.sandbox.nequi.com/payments/v2/-services-paymentservice-getstatuspayment`

  ### Cuerpo de la solicitud

  ```json
  {
    "RequestMessage":{
      "RequestHeader":{
        "Channel":"PNP04-C001",
        "RequestDate":"2025-01-20T14:28:05Z",
        "MessageID":"P2ZWAuzMAf",
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
            "codeQR":"350-12345-36517011-KDcyo8JTLc"
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
          "ResponseDate":"2025-01-20T14:28:10.267Z",
          "Status":{
            "StatusCode":"10-455",
            "StatusDesc":"La transacción esta cancelada"
          },
          "MessageID":"P2ZWAuzMAf",
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

## 4. Pagos expirados

- ### **Solicitud de notificación push**

  ### URL

  `https://api.sandbox.nequi.com/payments/v2/-services-paymentservice-unregisteredpayment`

  ### Cuerpo de la solicitud

  ```json
  {
    "RequestMessage":{
      "RequestHeader":{
        "Channel":"PNP04-C001",
        "RequestDate":"2025-01-20T21:49:10Z",
        "MessageID":"khHWnqdl1N",
        "ClientID":"12345",
        "Destination":{
          "ServiceName":"PaymentsService",
          "ServiceOperation":"unregisteredPayment",
          "ServiceRegion":"C001",
          "ServiceVersion":"1.0.0"
        }
      },
      "RequestBody":{
        "any":{
          "unregisteredPaymentRQ":{
            "phoneNumber":"3560567253",
            "code":"NIT_1",
            "value":"5950",
            "reference1":"reference1",
            "reference2":"reference2",
            "reference3":"reference3"
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
      "ResponseMessage":{
        "ResponseHeader":{
          "Channel":"PNP04-C001",
          "ResponseDate":"2025-01-20T21:49:14.290Z",
          "Status":{
            "StatusCode":"0",
            "StatusDesc":"SUCCESS"
          },
          "MessageID":"khHWnqdl1N",
          "ClientID":"12345",
          "Destination":{
            "ServiceName":"PaymentsService",
            "ServiceOperation":"unregisteredPayment",
            "ServiceRegion":"C001",
            "ServiceVersion":"1.0.0"
          }
        },
        "ResponseBody":{
          "any":{
            "unregisteredPaymentRS":{
              "transactionId":"350-12345-36517011-khHWnqdl1N"
            }
          }
        }
      }
    }
    ```

  - **ID de Transacción**: `350-12345-36517011-khHWnqdl1N`

- ### **Consultando Estado del Pago**

  ### URL

  `https://api.sandbox.nequi.com/payments/v2/-services-paymentservice-getstatuspayment`

  ### Cuerpo de la solicitud

  ```json
  {
    "RequestMessage":{
      "RequestHeader":{
        "Channel":"PNP04-C001",
        "RequestDate":"2025-01-20T22:04:16Z",
        "MessageID":"zOuwYK1y4o",
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
            "codeQR":"350-12345-36517011-khHWnqdl1N"
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
          "ResponseDate":"2025-01-20T22:04:21.722Z",
          "Status":{
            "StatusCode":"10-454",
            "StatusDesc":"La transacción ya caducó"
          },
          "MessageID":"zOuwYK1y4o",
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

  - **Estado del Pago**: `10-454`

---

## 5. Pagos con número que no tiene cuenta Nequi

- ### **Solicitud de notificación push**

  ### URL

  `https://api.sandbox.nequi.com/payments/v2/-services-paymentservice-unregisteredpayment`

  ### Cuerpo de la solicitud

  ```json
  {
    "RequestMessage":{
      "RequestHeader":{
        "Channel":"PNP04-C001",
        "RequestDate":"2025-01-20T14:46:36Z",
        "MessageID":"5PQEcaSRHj",
        "ClientID":"12345",
        "Destination":{
          "ServiceName":"PaymentsService",
          "ServiceOperation":"unregisteredPayment",
          "ServiceRegion":"C001",
          "ServiceVersion":"1.0.0"
        }
      },
      "RequestBody":{
        "any":{
          "unregisteredPaymentRQ":{
            "phoneNumber":"3222222222",
            "code":"NIT_1",
            "value":"5950",
            "reference1":"reference1",
            "reference2":"reference2",
            "reference3":"reference3"
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
      "ResponseMessage":{
        "ResponseHeader":{
          "Channel":"PNP04-C001",
          "ResponseDate":"2025-01-20T14:46:42.299Z",
          "Status":{
            "StatusCode":"20-08A",
            "StatusDesc":"Ese cliente no existe"
          },
          "MessageID":"5PQEcaSRHj",
          "ClientID":"12345",
          "Destination":{
            "ServiceName":"PaymentsService",
            "ServiceOperation":"unregisteredPayment",
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

  - **ID de Transacción**: `no registra`

---

## 6. Uso del servicio de reverso de pagos

- ### **Solicitud de notificación push**

  ### URL

  `https://api.sandbox.nequi.com/payments/v2/-services-paymentservice-unregisteredpayment`

  ### Cuerpo de la solicitud

  ```json
  {
    "RequestMessage":{
      "RequestHeader":{
        "Channel":"PNP04-C001",
        "RequestDate":"2025-01-21T14:00:14Z",
        "MessageID":"7XevoVtH5a",
        "ClientID":"12345",
        "Destination":{
          "ServiceName":"PaymentsService",
          "ServiceOperation":"unregisteredPayment",
          "ServiceRegion":"C001",
          "ServiceVersion":"1.0.0"
        }
      },
      "RequestBody":{
        "any":{
          "unregisteredPaymentRQ":{
            "phoneNumber":"3560567253",
            "code":"NIT_1",
            "value":"5950",
            "reference1":"reference1",
            "reference2":"reference2",
            "reference3":"reference3"
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
      "ResponseMessage":{
        "ResponseHeader":{
          "Channel":"PNP04-C001",
          "ResponseDate":"2025-01-21T14:00:26.235Z",
          "Status":{
            "StatusCode":"0",
            "StatusDesc":"SUCCESS"
          },
          "MessageID":"7XevoVtH5a",
          "ClientID":"12345",
          "Destination":{
            "ServiceName":"PaymentsService",
            "ServiceOperation":"unregisteredPayment",
            "ServiceRegion":"C001",
            "ServiceVersion":"1.0.0"
          }
        },
        "ResponseBody":{
          "any":{
            "unregisteredPaymentRS":{
              "transactionId":"350-12345-36517011-7XevoVtH5a"
            }
          }
        }
      }
    }
    ```

  - **ID de Transacción**: `350-12345-36517011-7XevoVtH5a`

- ### **Consultando Estado del Pago**

  ### URL

  `https://api.sandbox.nequi.com/payments/v2/-services-paymentservice-getstatuspayment`

  ### Cuerpo de la solicitud

  ```json
  {
    "RequestMessage":{
      "RequestHeader":{
        "Channel":"PNP04-C001",
        "RequestDate":"2025-01-21T14:03:28Z",
        "MessageID":"fM2xrJ9clv",
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
            "codeQR":"350-12345-36517011-7XevoVtH5a"
          }
        }
      }
    }
  }
  ```

  ### Respuesta obtenida

  - **Cuerpo de la respueta**:

    ```plaintext
      Net::ReadTimeout with #<TCPSocket:(closed)>
    ```

  - **Estado del Pago**: `nil`

    > **Nota:** Esta respuesta indica que no se pudo obtener el estado del pago debido a un tiempo de espera agotado durante la consulta. Esto puede ocurrir por problemas de conectividad o por una respuesta tardía del servicio externo.

- ### **Reversar pago**
  
  ### URL

  `https://api.sandbox.nequi.com/payments/v2/-services-reverseservices-reversetransaction`

  ### Cuerpo de la solicitud

  ```json
  {
    "RequestMessage":{
      "RequestHeader":{
        "Channel":"PNP04-C001",
        "RequestDate":"2025-01-21T14:03:32Z",
        "MessageID":"mfqB2lijuZ",
        "ClientID":"12345",
        "Destination":{
          "ServiceName":"ReverseServices",
          "ServiceOperation":"reverseTransaction",
          "ServiceRegion":"C001",
          "ServiceVersion":"1.0.0"
        }
      },
      "RequestBody":{
        "any":{
          "reversionRQ":{
            "phoneNumber":"3560567253",
            "value":"5950",
            "code":"NIT_1",
            "messageId":"7XevoVtH5a",
            "type":"payment"
          }
        }
      }
    }
  }
  ```

  ### Respuesta obtenida

  ```json
  {
    "ResponseMessage": {
      "ResponseHeader": {
        "Channel": "PNP04-C001",
        "ResponseDate": "2025-01-21T14:03:37.535Z",
        "Status": {
          "StatusCode": "0",
          "StatusDesc": "SUCCESS"
        },
        "MessageID": "mfqB2lijuZ",
        "ClientID": "12345",
        "Destination": {
          "ServiceName": "ReverseServices",
          "ServiceOperation": "reverseTransaction",
          "ServiceRegion": "C001",
          "ServiceVersion": "1.0.0"
        }
      },
      "ResponseBody": {
        "any": {
          "reversionRS": {}
        }
      }
    },
    "Headers": {
      "content-type": ["application/json"],
      "content-length": ["378"],
      "connection": ["close"],
      "date": ["Tue, 21 Jan 2025 14:03:37 GMT"],
      "x-amzn-trace-id": [
        "Root=1-678fa934-75ced580662766663ec6e042;Parent=49fe79d4a08c62cc;Sampled=0;Lineage=1:0ad258a9:0"
      ],
      "x-amzn-requestid": ["7aa6d893-6025-4302-ad3a-961fd535c900"],
      "access-control-allow-origin": ["*"],
      "x-amz-apigw-id": ["EvdgMFPgIAMEuJw="],
      "x-cache": ["Miss from cloudfront"],
      "via": [
        "1.1 4e6e9c8ad6e40529a0e7659f2f4c5f28.cloudfront.net (CloudFront)"
      ],
      "x-amz-cf-pop": ["IAD89-P2"],
      "x-amz-cf-id": [
        "HCGE27dA_h7HDiVWKP3rcHtNCmw_3olhKDoP2m3spVtbKt4BNN-hYw=="
      ]
    }
  }
  ```

---

## 7. Experiencia de usuario

- ### Elegir metodo de pago

  ![metodo_pago](images/metodo_pago.jpeg)

- ### Rellenar datos requeridos

  ![datos](images/datos_requerios.jpeg)

- ### Espera de confirmacion
  
  ![confirmacion](images/confirmacion_pago.jpeg)
