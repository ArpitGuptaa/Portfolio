{
    "openapi": "3.0.0",
    "info": {
        "title": "Transarmor Tokenization API",
        "version": "1.0.0"
    },
    "servers": [
        {
            "description": "Sandbox token server",
            "url": "https://token-sandbox.dev.clover.com"
        }
    ],
    "components": {
        "requestBodies": {
            "CreateTokenRequest": {
                "description": "Card details, including metadata of the tokenized card.",
                "required": true,
                "content": {
                    "application/json": {
                        "encoding": {
                            "expand": {
                                "explode": true,
                                "style": "deepObject"
                            },
                            "items": {
                                "explode": true,
                                "style": "deepObject"
                            },
                            "metadata": {
                                "explode": true,
                                "style": "deepObject"
                            },
                            "shipping": {
                                "explode": true,
                                "style": "deepObject"
                            }
                        },
                        "schema": {
                            "properties": {
                                "card": {
                                    "required": [
                                        "first6",
                                        "last4",
                                        "exp_month",
                                        "exp_year",
                                        "cvv",
                                        "brand"
                                    ],
                                    "description": "Card details, including metadata of the tokenized card.",
                                    "type": "object",
                                    "properties": {
                                        "number": {
                                            "type": "string",
                                            "description": "Card primary account number (PAN). To minimize your app's payment card industry (PCI) compliance burden, use `encrypted_pan` instead."
                                        },
                                        "encrypted_pan": {
                                            "description": "Encrypted card primary account number (PAN). See [Generating a card token](https://docs.clover.com/docs/ecommerce-generating-a-card-token) for steps to encrypt card data.",
                                            "type": "string"
                                        },
                                        "exp_month": {
                                            "description": "Card expiration month in 2-digit format.",
                                            "type": "string"
                                        },
                                        "exp_year": {
                                            "description": "Card expiration year in 2-or 4-digit format.",
                                            "type": "string"
                                        },
                                        "cvv": {
                                            "description": "Card verification value (CVV). A 3-digit value printed on a card.",
                                            "type": "string"
                                        },
                                        "last4": {
                                            "description": "Last 4 numbers of the primary account number.",
                                            "type": "string"
                                        },
                                        "first6": {
                                            "description": "First 6 numbers of the primary account number.",
                                            "type": "string"
                                        },
                                        "country": {
                                            "description": "2-character country code.",
                                            "type": "string"
                                        },
                                        "brand": {
                                            "description": "Card brand.",
                                            "type": "string",
                                            "enum": [
                                                "VISA",
                                                "MC",
                                                "AMEX",
                                                "DISCOVER",
                                                "DINERS_CLUB",
                                                "JCB"
                                            ]
                                        },
                                        "name": {
                                            "description": "Cardholder's full name on the card.",
                                            "type": "string"
                                        },
                                        "address_line1": {
                                            "description": "First line of the address. Can include the street address, PO box, or company name.",
                                            "type": "string"
                                        },
                                        "address_line2": {
                                            "description": "Second line of the address. Can include the apartment, suite, unit, or building number.",
                                            "type": "string"
                                        },
                                        "address_city": {
                                            "description": "City of the customer address. Can include district, suburb, town, or village.",
                                            "type": "string"
                                        },
                                        "address_state": {
                                            "description": "State of the customer address. Can include county, province, or region.",
                                            "type": "string"
                                        },
                                        "address_zip": {
                                            "description": "State of the customer address. Can include county, province, or region.",
                                            "type": "string"
                                        },
                                        "address_country": {
                                            "description": "Billing address country, if provided.",
                                            "type": "string"
                                        }
                                    }
                                }
                            }
                        }
                    }
                }
            }
        },
        "schemas": {
            "error": {
                "description": "An error response from the API.",
                "properties": {
                    "type": {
                        "description": "Error type.",
                        "enum": [
                            "api_connection_error",
                            "api_error",
                            "authentication_error",
                            "card_error",
                            "idempotency_error",
                            "invalid_request_error",
                            "rate_limit_error",
                            "validation_error"
                        ]
                    },
                    "code": {
                        "description": "Error codes. Additional information about the error that users can use to identify the issue.",
                        "enum": [
                            "amount_too_large",
                            "amount_too_small",
                            "api_key_expired",
                            "card_declined",
                            "charge_already_captured",
                            "charge_already_refunded",
                            "charge_disputed",
                            "charge_exceeds_source_limit",
                            "charge_expired_for_capture",
                            "country_unsupported",
                            "email_invalid",
                            "expired_card",
                            "incorrect_address",
                            "incorrect_cvc",
                            "incorrect_number",
                            "incorrect_zip",
                            "invalid_card_type",
                            "invalid_charge_amount",
                            "invalid_cvc",
                            "invalid_expiry_month",
                            "invalid_expiry_year",
                            "invalid_number",
                            "missing",
                            "order_creation_failed",
                            "order_required_settings",
                            "order_status_invalid",
                            "parameter_invalid_empty",
                            "parameter_invalid_integer",
                            "parameter_invalid_string_blank",
                            "parameter_invalid_string_empty",
                            "parameter_missing",
                            "parameter_unknown",
                            "postal_code_invalid",
                            "processing_error",
                            "rate_limit",
                            "resource_missing",
                            "token_already_used",
                            "invalid_request"
                        ]
                    },
                    "message": {
                        "description": "Detailed information about the error code.",
                        "type": "string"
                    },
                    "decline_code": {
                        "description": "Displays when a card issuer declines the transaction. This includes the reason for the decline if specified by the card issuer.",
                        "type": "string"
                    },
                    "charge": {
                        "description": "Displays for card-related errors. Unique identifier (ID) of the failed charge.",
                        "type": "string"
                    },
                    "doc_url": {
                        "description": "Link (URL) for more information about the reported error code.",
                        "type": "string"
                    },
                    "param": {
                        "description": "Displays for card parameter errors. The error message can inform users entering card information of a specific problem with their entry.",
                        "type": "string"
                    }
                }
            },
            "CreateTokenResponse": {
                "properties": {
                    "id": {
                        "description": "Unique identification.",
                        "maxLength": 128,
                        "type": "string"
                    },
                    "token": {
                        "description": "Public source token provided by Clover.",
                        "maxLength": 128,
                        "type": "string"
                    },
                    "card": {
                        "description": "Card details, including metadata of the tokenized card.",
                        "properties": {
                            "number": {
                                "description": "Card number.",
                                "type": "string"
                            },
                            "encrypted_pan": {
                                "description": "Encrypted card primary account number (PAN) provided by TransArmor.",
                                "type": "string"
                            },
                            "exp_month": {
                                "description": "Card expiration month in 2-digit format-(MM).",
                                "type": "string"
                            },
                            "exp_year": {
                                "description": "Card expiration year in 2- or 4- digit format-(YYYY).",
                                "type": "string"
                            },
                            "cvv": {
                                "description": "Card verification value.",
                                "type": "string"
                            },
                            "last4": {
                                "description": "Last 4 numbers of the primary account number.",
                                "type": "string"
                            },
                            "first6": {
                                "description": "First 6 numbers of the primary account number.",
                                "type": "string"
                            },
                            "country": {
                                "description": "2-character country code.",
                                "type": "string"
                            },
                            "brand": {
                                "description": "Card brand.",
                                "type": "string",
                                "enum": [
                                    "VISA",
                                    "MC",
                                    "AMEX",
                                    "DISCOVER",
                                    "DINERS_CLUB",
                                    "JCB"
                                ]
                            },
                            "id": {
                                "description": "Unique identifier.",
                                "type": "string"
                            },
                            "object": {
                                "description": "Object type. Objects with the same type have the same value.",
                                "type": "string"
                            },
                            "name": {
                                "description": "Cardholder's full name.",
                                "type": "string"
                            },
                            "address_line1": {
                                "description": "Address line 1 (Street address/P.O. Box/Company name).",
                                "type": "string"
                            },
                            "address_line2": {
                                "description": "Address line 2 (Apartment/Suite/Unit/Building).",
                                "type": "string"
                            },
                            "address_city": {
                                "description": "City/District/Suburb/Town/Village.",
                                "type": "string"
                            },
                            "address_state": {
                                "description": "State/County/Province/Region.",
                                "type": "string"
                            },
                            "address_zip": {
                                "description": "ZIP or postal code.",
                                "type": "string"
                            },
                            "address_country": {
                                "description": "Billing address country, if provided.",
                                "type": "string"
                            },
                            "cvc_check": {
                                "description": "Results of the card verification code (CVC) check when a card payment is submitted to a card network for authorization. The card issuer checks the CVC against the information on file for the cardholder.",
                                "type": "string",
                                "enum": [
                                    "pass",
                                    "fail",
                                    "unavailable",
                                    "unchecked"
                                ]
                            }
                        }
                    },
                    "client_ip": {
                        "description": "Internet protocol (IP) address of the client generating the token.",
                        "maxLength": 45,
                        "type": "string"
                    },
                    "created": {
                        "description": "Time the token object was created.",
                        "format": "unix-time",
                        "type": "integer"
                    },
                    "livemode": {
                        "description": "Indicates whether the token object is live in production. Set to true if the token object is in production. Set to false if the object is in sandbox.",
                        "type": "boolean"
                    },
                    "type": {
                        "description": "Token type.",
                        "type": "string",
                        "enum": [
                            "card",
                            "wallet (Google Pay or Apple Pay)"
                        ]
                    },
                    "used": {
                        "description": "Indicates if the token is used. Note that tokens can be used only once.",
                        "type": "boolean"
                    }
                }
            },
            "CloverToken": {
                "properties": {
                    "id": {
                        "description": "Unique ID",
                        "type": "string",
                        "maxLength": 128
                    },
                    "tokenValue": {
                        "description": "Public source token by Clover",
                        "type": "string"
                    },
                    "merchantUuid": {
                        "description": "Merchant UUID",
                        "type": "string"
                    },
                    "developerAppUuid": {
                        "description": "Developer UUID",
                        "type": "string"
                    },
                    "createdTime": {
                        "type": "integer"
                    },
                    "lastAccessedTime": {
                        "type": "integer"
                    }
                }
            },
            "MultiPayToken": {
                "properties": {
                    "id": {
                        "description": "Unique ID",
                        "type": "string",
                        "maxLength": 13
                    },
                    "tokenValue": {
                        "description": "Private HSM encrypted token value provided by TransArmor",
                        "type": "string"
                    },
                    "tokenValueBackup": {
                        "description": "Private RSA encrypted token value provided by TransArmor",
                        "type": "string"
                    },
                    "taTokenType": {
                        "description": "TransArmor token type",
                        "type": "string"
                    },
                    "createdTime": {
                        "type": "integer"
                    },
                    "modifiedTime": {
                        "type": "integer"
                    }
                }
            },
            "TokenMeta": {
                "properties": {
                    "id": {
                        "description": "Unique ID",
                        "type": "string",
                        "maxLength": 13
                    },
                    "cloverTokenId": {
                        "description": "Meta ID of the token stored by Clover",
                        "type": "integer"
                    },
                    "tokenStatus": {
                        "type": "string",
                        "enum": [
                            "NEW",
                            "VERIFIED"
                        ]
                    },
                    "tokenType": {
                        "type": "string",
                        "enum": [
                            "ONEOFF",
                            "MULTIPAY",
                            "RECURRING"
                        ]
                    },
                    "tokenProvider": {
                        "type": "string",
                        "enum": [
                            "TASTM",
                            "IPG",
                            "MOCK"
                        ]
                    },
                    "paymentInstrument": {
                        "type": "string",
                        "enum": [
                            "CARD"
                        ]
                    },
                    "createdTime": {
                        "type": "integer"
                    },
                    "modifiedTime": {
                        "type": "integer"
                    }
                }
            },
            "Token": {
                "properties": {
                    "card": {
                        "description": "Card details, including metadata of the tokenized card.",
                        "properties": {
                            "number": {
                                "description": "Card number.",
                                "type": "string"
                            },
                            "encrypted_pan": {
                                "description": "Encrypted card primary account number (PAN) provided by TransArmor.",
                                "type": "string"
                            },
                            "exp_month": {
                                "description": "Card expiration month in 2-digit format-(MM).",
                                "type": "string"
                            },
                            "exp_year": {
                                "description": "Card expiration year in 2- or 4- digit format-(YYYY).",
                                "type": "string"
                            },
                            "cvv": {
                                "description": "Card verification value.",
                                "type": "string"
                            },
                            "last4": {
                                "description": "Last 4 numbers of the primary account number.",
                                "type": "string"
                            },
                            "first6": {
                                "description": "First 6 numbers of the primary account number.",
                                "type": "string"
                            },
                            "country": {
                                "description": "2-character country code.",
                                "type": "string"
                            },
                            "brand": {
                                "description": "Card brand.",
                                "type": "string",
                                "enum": [
                                    "VISA",
                                    "MC",
                                    "AMEX",
                                    "DISCOVER",
                                    "DINERS_CLUB",
                                    "JCB"
                                ]
                            },
                            "id": {
                                "description": "Unique identifier.",
                                "type": "string"
                            },
                            "object": {
                                "description": "Object type. Objects with the same type have the same value.",
                                "type": "string"
                            },
                            "name": {
                                "description": "Cardholder's full name.",
                                "type": "string"
                            },
                            "address_line1": {
                                "description": "Address line 1 (Street address/P.O. Box/Company name).",
                                "type": "string"
                            },
                            "address_line2": {
                                "description": "Address line 2 (Apartment/Suite/Unit/Building).",
                                "type": "string"
                            },
                            "address_city": {
                                "description": "City/District/Suburb/Town/Village.",
                                "type": "string"
                            },
                            "address_state": {
                                "description": "State/County/Province/Region.",
                                "type": "string"
                            },
                            "address_zip": {
                                "description": "ZIP or postal code.",
                                "type": "string"
                            },
                            "address_country": {
                                "description": "Billing address country, if provided.",
                                "type": "string"
                            },
                            "cvc_check": {
                                "description": "Results of the card verification code (CVC) check when a card payment is submitted to a card network for authorization. The card issuer checks the CVC against the information on file for the cardholder.",
                                "type": "string",
                                "enum": [
                                    "pass",
                                    "fail",
                                    "unavailable",
                                    "unchecked"
                                ]
                            }
                        }
                    },
                    "cloverToken": {
                        "properties": {
                            "id": {
                                "description": "Unique ID",
                                "type": "string",
                                "maxLength": 128
                            },
                            "tokenValue": {
                                "description": "Public source token by Clover",
                                "type": "string"
                            },
                            "merchantUuid": {
                                "description": "Merchant UUID",
                                "type": "string"
                            },
                            "developerAppUuid": {
                                "description": "Developer UUID",
                                "type": "string"
                            },
                            "createdTime": {
                                "type": "integer"
                            },
                            "lastAccessedTime": {
                                "type": "integer"
                            }
                        }
                    },
                    "multipayToken": {
                        "properties": {
                            "id": {
                                "description": "Unique ID",
                                "type": "string",
                                "maxLength": 13
                            },
                            "tokenValue": {
                                "description": "Private HSM encrypted token value provided by TransArmor",
                                "type": "string"
                            },
                            "tokenValueBackup": {
                                "description": "Private RSA encrypted token value provided by TransArmor",
                                "type": "string"
                            },
                            "taTokenType": {
                                "description": "TransArmor token type",
                                "type": "string"
                            },
                            "createdTime": {
                                "type": "integer"
                            },
                            "modifiedTime": {
                                "type": "integer"
                            }
                        }
                    },
                    "tokenMeta": {
                        "properties": {
                            "id": {
                                "description": "Unique ID",
                                "type": "string",
                                "maxLength": 13
                            },
                            "cloverTokenId": {
                                "description": "Meta ID of the token stored by Clover",
                                "type": "integer"
                            },
                            "tokenStatus": {
                                "type": "string",
                                "enum": [
                                    "NEW",
                                    "VERIFIED"
                                ]
                            },
                            "tokenType": {
                                "type": "string",
                                "enum": [
                                    "ONEOFF",
                                    "MULTIPAY",
                                    "RECURRING"
                                ]
                            },
                            "tokenProvider": {
                                "type": "string",
                                "enum": [
                                    "TASTM",
                                    "IPG",
                                    "MOCK"
                                ]
                            },
                            "paymentInstrument": {
                                "type": "string",
                                "enum": [
                                    "CARD"
                                ]
                            },
                            "createdTime": {
                                "type": "integer"
                            },
                            "modifiedTime": {
                                "type": "integer"
                            }
                        }
                    }
                }
            },
            "UpdateTokenRequest": {
                "additionalProperties": false,
                "properties": {
                    "token": {
                        "description": "Public source token by Clover",
                        "maxLength": 128,
                        "type": "string"
                    },
                    "type": {
                        "type": "string",
                        "enum": [
                            "ONEOFF",
                            "MULTIPAY",
                            "RECURRING"
                        ]
                    }
                }
            },
            "Card": {
                "description": "Card details, including metadata of the tokenized card.",
                "properties": {
                    "number": {
                        "description": "Card number.",
                        "type": "string"
                    },
                    "encrypted_pan": {
                        "description": "Encrypted card primary account number (PAN) provided by TransArmor.",
                        "type": "string"
                    },
                    "exp_month": {
                        "description": "Card expiration month in 2-digit format-(MM).",
                        "type": "string"
                    },
                    "exp_year": {
                        "description": "Card expiration year in 2- or 4- digit format-(YYYY).",
                        "type": "string"
                    },
                    "cvv": {
                        "description": "Card verification value.",
                        "type": "string"
                    },
                    "last4": {
                        "description": "Last 4 numbers of the primary account number.",
                        "type": "string"
                    },
                    "first6": {
                        "description": "First 6 numbers of the primary account number.",
                        "type": "string"
                    },
                    "country": {
                        "description": "2-character country code.",
                        "type": "string"
                    },
                    "brand": {
                        "description": "Card brand.",
                        "type": "string",
                        "enum": [
                            "VISA",
                            "MC",
                            "AMEX",
                            "DISCOVER",
                            "DINERS_CLUB",
                            "JCB"
                        ]
                    },
                    "id": {
                        "description": "Unique identifier.",
                        "type": "string"
                    },
                    "object": {
                        "description": "Object type. Objects with the same type have the same value.",
                        "type": "string"
                    },
                    "name": {
                        "description": "Cardholder's full name.",
                        "type": "string"
                    },
                    "address_line1": {
                        "description": "Address line 1 (Street address/P.O. Box/Company name).",
                        "type": "string"
                    },
                    "address_line2": {
                        "description": "Address line 2 (Apartment/Suite/Unit/Building).",
                        "type": "string"
                    },
                    "address_city": {
                        "description": "City/District/Suburb/Town/Village.",
                        "type": "string"
                    },
                    "address_state": {
                        "description": "State/County/Province/Region.",
                        "type": "string"
                    },
                    "address_zip": {
                        "description": "ZIP or postal code.",
                        "type": "string"
                    },
                    "address_country": {
                        "description": "Billing address country, if provided.",
                        "type": "string"
                    },
                    "cvc_check": {
                        "description": "Results of the card verification code (CVC) check when a card payment is submitted to a card network for authorization. The card issuer checks the CVC against the information on file for the cardholder.",
                        "type": "string",
                        "enum": [
                            "pass",
                            "fail",
                            "unavailable",
                            "unchecked"
                        ]
                    }
                }
            },
            "CardType": {
                "description": "Card brand.",
                "type": "string",
                "enum": [
                    "VISA",
                    "MC",
                    "AMEX",
                    "DISCOVER",
                    "DINERS_CLUB",
                    "JCB"
                ]
            },
            "TokenType": {
                "type": "string",
                "enum": [
                    "ONEOFF",
                    "MULTIPAY",
                    "RECURRING"
                ]
            },
            "CheckType": {
                "description": "Indicates whether bank account is a personal or a business account.\n Values:\n - personal_check (first name, last name, and email required)\n  - corporate_check (first name, last name, and email not required).",
                "type": "string",
                "enum": [
                    "personal_check (first name, last name, and email required)",
                    "corporate_check (first name, last name, and email not required)"
                ]
            },
            "AccountType": {
                "description": "Indicates whether bank account is a checking or a savings account.\n Values:\n - Savings\n - Checking",
                "type": "string",
                "enum": [
                    "savings",
                    "checking"
                ]
            },
            "CustomerIdType": {
                "description": "Indicates the type of customer ID, for example, driver_license, ssn, tax_id, or miilitary_id).",
                "type": "string",
                "enum": [
                    "driver_license",
                    "ssn",
                    "tax_id",
                    "military_id"
                ]
            }
        }
    },
    "paths": {
        "/v1/tokens": {
            "post": {
                "tags": [
                    "TOKENS"
                ],
                "operationId": "CreateToken",
                "summary": "Create a Transarmor token",
                "x-clover-handler": "com.clover.tokenization.handler.CreateTokenHandler",
                "x-clover-is-public": true,
                "description": "Creates a single-pay token to use in the Clover Ecommerce network.",
                "parameters": [
                    {
                        "in": "header",
                        "name": "apikey",
                        "description": "Universally unique identifier (ID) of the API.",
                        "schema": {
                            "type": "string",
                            "format": "uuid"
                        },
                        "required": true
                    }
                ],
                "requestBody": {
                    "required": true,
                    "content": {
                        "application/json": {
                            "encoding": {
                                "expand": {
                                    "explode": true,
                                    "style": "deepObject"
                                },
                                "items": {
                                    "explode": true,
                                    "style": "deepObject"
                                },
                                "metadata": {
                                    "explode": true,
                                    "style": "deepObject"
                                },
                                "shipping": {
                                    "explode": true,
                                    "style": "deepObject"
                                }
                            },
                            "schema": {
                                "properties": {
                                    "card": {
                                        "required": [
                                            "number",
                                            "first6",
                                            "last4",
                                            "exp_month",
                                            "exp_year",
                                            "cvv"
                                        ],
                                        "description": "Card details, including metadata of the tokenized card.",
                                        "type": "object",
                                        "properties": {
                                            "number": {
                                                "type": "string",
                                                "description": "Card primary account number (PAN). To minimize your app's payment card industry (PCI) compliance burden, use `encrypted_pan` instead."
                                            },
                                            "encrypted_pan": {
                                                "description": "Encrypted card primary account number (PAN). See [Generate a card token](https://docs.clover.com/docs/ecommerce-generating-a-card-token) for steps to encrypt card data.",
                                                "type": "string"
                                            },
                                            "exp_month": {
                                                "description": "Card expiration month in 2-digit format.\n Format: mm",
                                                "type": "string"
                                            },
                                            "exp_year": {
                                                "description": "Card expiration year in 2- or 4-digit format.\n Format: yy or yyyy",
                                                "type": "string"
                                            },
                                            "cvv": {
                                                "description": "Card verification value (CVV). A 3-digit value printed on a card.",
                                                "type": "string"
                                            },
                                            "last4": {
                                                "description": "Last 4 numbers of the primary account number.",
                                                "type": "string"
                                            },
                                            "first6": {
                                                "description": "First 6 numbers of the primary account number.",
                                                "type": "string"
                                            },
                                            "country": {
                                                "description": "2-character country code.",
                                                "type": "string"
                                            },
                                            "brand": {
                                                "description": "Card brand.",
                                                "type": "string",
                                                "enum": [
                                                    "VISA",
                                                    "MC",
                                                    "AMEX",
                                                    "DISCOVER",
                                                    "DINERS_CLUB",
                                                    "JCB"
                                                ]
                                            },
                                            "name": {
                                                "description": "Cardholder's full name on the card.",
                                                "type": "string"
                                            },
                                            "address_line1": {
                                                "description": "First line of the address. Can include the street address, PO box, or company name.",
                                                "type": "string"
                                            },
                                            "address_line2": {
                                                "description": "Second line of the address. Can include the apartment, suite, unit, or building number.",
                                                "type": "string"
                                            },
                                            "address_city": {
                                                "description": "City of the customer address. Can include district, suburb, town, or village.",
                                                "type": "string"
                                            },
                                            "address_state": {
                                                "description": "State of the customer address. Can include county, province, or region.",
                                                "type": "string"
                                            },
                                            "address_zip": {
                                                "description": "State of the customer address. Can include county, province, or region.",
                                                "type": "string"
                                            },
                                            "address_country": {
                                                "description": "Billing address country, if provided.",
                                                "type": "string"
                                            }
                                        }
                                    },
                                    "external_token": {
                                        "required": [
                                            "token_value",
                                            "token_type",
                                            "transarmor_token_attribute"
                                        ],
                                        "description": "External token details, including metadata of the card.",
                                        "type": "object",
                                        "properties": {
                                            "token_value": {
                                                "type": "integer",
                                                "description": "Value of the mutlipay token."
                                            },
                                            "transarmor_token_attribute": {
                                                "type": "object",
                                                "required": [
                                                    "exp_month",
                                                    "exp_year"
                                                ],
                                                "properties": {
                                                    "exp_month": {
                                                        "type": "string",
                                                        "description": "Card expiration month in 2-digit format.\n Format: mm"
                                                    },
                                                    "exp_year": {
                                                        "type": "string",
                                                        "description": "Card expiration year in 2- or 4-digit format.\n Format: Format: yy or yyyy"
                                                    },
                                                    "name": {
                                                        "type": "string",
                                                        "description": "Cardholder's full name on the card."
                                                    },
                                                    "brand": {
                                                        "type": "string",
                                                        "description": "Card brand.",
                                                        "enum": [
                                                            "VISA",
                                                            "MC",
                                                            "AMEX",
                                                            "DISCOVER",
                                                            "DINERS_CLUB",
                                                            "JCB"
                                                        ]
                                                    },
                                                    "first6": {
                                                        "type": "string",
                                                        "description": "First 6 numbers of the primary account number."
                                                    },
                                                    "last4": {
                                                        "type": "string",
                                                        "description": "Last 4 numbers of the primary account number."
                                                    },
                                                    "address_line1": {
                                                        "type": "string",
                                                        "description": "First line of the address. Can include the street address, PO box, or company name."
                                                    },
                                                    "address_line2": {
                                                        "description": "Second line of the address. Can include the apartment, suite, unit, or building number.",
                                                        "type": "string"
                                                    },
                                                    "address_city": {
                                                        "description": "City of the customer address. Can include district, suburb, town, or village.",
                                                        "type": "string"
                                                    },
                                                    "address_state": {
                                                        "description": "State of the customer address. Can include county, province, or region.",
                                                        "type": "string"
                                                    },
                                                    "address_zip": {
                                                        "description": "State of the customer address. Can include county, province, or region.",
                                                        "type": "string"
                                                    },
                                                    "address_country": {
                                                        "description": "Billing address country, if provided.",
                                                        "type": "string"
                                                    },
                                                    "transactionId": {
                                                        "description": "Initial transaction identifier received from Rapid Connect transaction response.",
                                                        "type": "string"
                                                    }
                                                }
                                            }
                                        }
                                    }
                                }
                            }
                        }
                    }
                },
                "responses": {
                    "200": {
                        "description": "Successful response.",
                        "content": {
                            "application/json": {
                                "schema": {
                                    "properties": {
                                        "id": {
                                            "description": "Unique identification.",
                                            "maxLength": 128,
                                            "type": "string"
                                        },
                                        "token": {
                                            "description": "Public source token provided by Clover.",
                                            "maxLength": 128,
                                            "type": "string"
                                        },
                                        "card": {
                                            "description": "Card details, including metadata of the tokenized card.",
                                            "properties": {
                                                "number": {
                                                    "description": "Card number.",
                                                    "type": "string"
                                                },
                                                "encrypted_pan": {
                                                    "description": "Encrypted card primary account number (PAN) provided by TransArmor®.",
                                                    "type": "string"
                                                },
                                                "exp_month": {
                                                    "description": "Card expiration month in 2-digit format.\n Format: mm",
                                                    "type": "string"
                                                },
                                                "exp_year": {
                                                    "description": "Card expiration year in 2- or 4- digit.\n Format: yy or yyyy",
                                                    "type": "string"
                                                },
                                                "cvv": {
                                                    "description": "Card verification value.",
                                                    "type": "string"
                                                },
                                                "last4": {
                                                    "description": "Last 4 numbers of the primary account number.",
                                                    "type": "string"
                                                },
                                                "first6": {
                                                    "description": "First 6 numbers of the primary account number.",
                                                    "type": "string"
                                                },
                                                "country": {
                                                    "description": "2-character country code.",
                                                    "type": "string"
                                                },
                                                "brand": {
                                                    "description": "Card brand.",
                                                    "type": "string",
                                                    "enum": [
                                                        "VISA",
                                                        "MC",
                                                        "AMEX",
                                                        "DISCOVER",
                                                        "DINERS_CLUB",
                                                        "JCB"
                                                    ]
                                                },
                                                "id": {
                                                    "description": "Unique identifier.",
                                                    "type": "string"
                                                },
                                                "object": {
                                                    "description": "Object type. Objects with the same type have the same value.",
                                                    "type": "string"
                                                },
                                                "name": {
                                                    "description": "Cardholder's full name.",
                                                    "type": "string"
                                                },
                                                "address_line1": {
                                                    "description": "First line of the address. Can include the street address, PO box, or company name.",
                                                    "type": "string"
                                                },
                                                "address_line2": {
                                                    "description": "Second line of the address. Can include the apartment, suite, unit, or building number.",
                                                    "type": "string"
                                                },
                                                "address_city": {
                                                    "description": "City of the customer address. Can include district, suburb, town, or village.",
                                                    "type": "string"
                                                },
                                                "address_state": {
                                                    "description": "State of the customer address. Can include county, province, or region.",
                                                    "type": "string"
                                                },
                                                "address_zip": {
                                                    "description": "State of the customer address. Can include county, province, or region.",
                                                    "type": "string"
                                                },
                                                "address_country": {
                                                    "description": "Billing address country, if provided.",
                                                    "type": "string"
                                                },
                                                "cvc_check": {
                                                    "description": "Results of the card verification code (CVC) check when a card payment is submitted to a card network for authorization. The card issuer checks the CVC against the information on file for the cardholder.",
                                                    "type": "string",
                                                    "enum": [
                                                        "pass",
                                                        "fail",
                                                        "unavailable",
                                                        "unchecked"
                                                    ]
                                                }
                                            }
                                        },
                                        "client_ip": {
                                            "description": "Internet protocol (IP) address of the client generating the token.",
                                            "maxLength": 45,
                                            "type": "string"
                                        },
                                        "created": {
                                            "description": "Time the token object was created.",
                                            "format": "unix-time",
                                            "type": "integer"
                                        },
                                        "livemode": {
                                            "description": "Indicates whether the token object is live in production.\n Values: \n True - Token object is in production. \n False - Token object is in sandbox.",
                                            "type": "boolean"
                                        },
                                        "type": {
                                            "description": "Token type.",
                                            "type": "string",
                                            "enum": [
                                                "card",
                                                "wallet (Google Pay or Apple Pay)"
                                            ]
                                        },
                                        "used": {
                                            "description": "Indicates whether the token is already used. Note that tokens can be used only once.",
                                            "type": "boolean"
                                        }
                                    }
                                }
                            }
                        }
                    },
                    "400": {
                        "content": {
                            "application/json": {
                                "schema": {
                                    "description": "An error response from the API.",
                                    "properties": {
                                        "type": {
                                            "description": "Error type.",
                                            "enum": [
                                                "api_connection_error",
                                                "api_error",
                                                "authentication_error",
                                                "card_error",
                                                "idempotency_error",
                                                "invalid_request_error",
                                                "rate_limit_error",
                                                "validation_error"
                                            ]
                                        },
                                        "code": {
                                            "description": "Error codes. Additional information about the error that users can use to identify the issue.",
                                            "enum": [
                                                "amount_too_large",
                                                "amount_too_small",
                                                "api_key_expired",
                                                "card_declined",
                                                "charge_already_captured",
                                                "charge_already_refunded",
                                                "charge_disputed",
                                                "charge_exceeds_source_limit",
                                                "charge_expired_for_capture",
                                                "country_unsupported",
                                                "email_invalid",
                                                "expired_card",
                                                "incorrect_address",
                                                "incorrect_cvc",
                                                "incorrect_number",
                                                "incorrect_zip",
                                                "invalid_card_type",
                                                "invalid_charge_amount",
                                                "invalid_cvc",
                                                "invalid_expiry_month",
                                                "invalid_expiry_year",
                                                "invalid_number",
                                                "missing",
                                                "order_creation_failed",
                                                "order_required_settings",
                                                "order_status_invalid",
                                                "parameter_invalid_empty",
                                                "parameter_invalid_integer",
                                                "parameter_invalid_string_blank",
                                                "parameter_invalid_string_empty",
                                                "parameter_missing",
                                                "parameter_unknown",
                                                "postal_code_invalid",
                                                "processing_error",
                                                "rate_limit",
                                                "resource_missing",
                                                "token_already_used",
                                                "invalid_request"
                                            ]
                                        },
                                        "message": {
                                            "description": "Detailed information about the error code.",
                                            "type": "string"
                                        },
                                        "decline_code": {
                                            "description": "Displays when a card issuer declined the transaction. This includes the reason for the decline if specified by the card issuer.",
                                            "type": "string"
                                        },
                                        "charge": {
                                            "description": "Displays for card-related errors. Unique identifier (ID) of the failed charge.",
                                            "type": "string"
                                        },
                                        "doc_url": {
                                            "description": "Link (URL) for more information about the reported error code.",
                                            "type": "string"
                                        },
                                        "param": {
                                            "description": "Displays for card parameter errors. The error message can inform users entering card information of a specific problem with their entry.",
                                            "type": "string"
                                        }
                                    }
                                }
                            }
                        },
                        "description": "Bad request."
                    },
                    "401": {
                        "content": {
                            "application/json": {
                                "schema": {
                                    "description": "An error response from the API.",
                                    "properties": {
                                        "type": {
                                            "description": "Error type.",
                                            "enum": [
                                                "api_connection_error",
                                                "api_error",
                                                "authentication_error",
                                                "card_error",
                                                "idempotency_error",
                                                "invalid_request_error",
                                                "rate_limit_error",
                                                "validation_error"
                                            ]
                                        },
                                        "code": {
                                            "description": "Error codes. Additional information about the error that users can use to identify the issue.",
                                            "enum": [
                                                "amount_too_large",
                                                "amount_too_small",
                                                "api_key_expired",
                                                "card_declined",
                                                "charge_already_captured",
                                                "charge_already_refunded",
                                                "charge_disputed",
                                                "charge_exceeds_source_limit",
                                                "charge_expired_for_capture",
                                                "country_unsupported",
                                                "email_invalid",
                                                "expired_card",
                                                "incorrect_address",
                                                "incorrect_cvc",
                                                "incorrect_number",
                                                "incorrect_zip",
                                                "invalid_card_type",
                                                "invalid_charge_amount",
                                                "invalid_cvc",
                                                "invalid_expiry_month",
                                                "invalid_expiry_year",
                                                "invalid_number",
                                                "missing",
                                                "order_creation_failed",
                                                "order_required_settings",
                                                "order_status_invalid",
                                                "parameter_invalid_empty",
                                                "parameter_invalid_integer",
                                                "parameter_invalid_string_blank",
                                                "parameter_invalid_string_empty",
                                                "parameter_missing",
                                                "parameter_unknown",
                                                "postal_code_invalid",
                                                "processing_error",
                                                "rate_limit",
                                                "resource_missing",
                                                "token_already_used",
                                                "invalid_request"
                                            ]
                                        },
                                        "message": {
                                            "description": "Detailed information about the error code.",
                                            "type": "string"
                                        },
                                        "decline_code": {
                                            "description": "Displays when a card issuer declines the transaction. This includes the reason for the decline if specified by the card issuer.",
                                            "type": "string"
                                        },
                                        "charge": {
                                            "description": "Displays for card-related errors. Unique identifier (ID) of the failed charge.",
                                            "type": "string"
                                        },
                                        "doc_url": {
                                            "description": "Link (URL) for more information about the reported error code.",
                                            "type": "string"
                                        },
                                        "param": {
                                            "description": "Displays for card parameter errors. The error message can inform users entering card information of a specific problem with their entry.",
                                            "type": "string"
                                        }
                                    }
                                }
                            }
                        },
                        "description": "Authorization information is missing or invalid."
                    },
                    "5XX": {
                        "content": {
                            "application/json": {
                                "schema": {
                                    "description": "An error response from the API.",
                                    "properties": {
                                        "type": {
                                            "description": "Error type.",
                                            "enum": [
                                                "api_connection_error",
                                                "api_error",
                                                "authentication_error",
                                                "card_error",
                                                "idempotency_error",
                                                "invalid_request_error",
                                                "rate_limit_error",
                                                "validation_error"
                                            ]
                                        },
                                        "code": {
                                            "description": "Error codes. Additional information about the error that users can use to identify the issue.",
                                            "enum": [
                                                "amount_too_large",
                                                "amount_too_small",
                                                "api_key_expired",
                                                "card_declined",
                                                "charge_already_captured",
                                                "charge_already_refunded",
                                                "charge_disputed",
                                                "charge_exceeds_source_limit",
                                                "charge_expired_for_capture",
                                                "country_unsupported",
                                                "email_invalid",
                                                "expired_card",
                                                "incorrect_address",
                                                "incorrect_cvc",
                                                "incorrect_number",
                                                "incorrect_zip",
                                                "invalid_card_type",
                                                "invalid_charge_amount",
                                                "invalid_cvc",
                                                "invalid_expiry_month",
                                                "invalid_expiry_year",
                                                "invalid_number",
                                                "missing",
                                                "order_creation_failed",
                                                "order_required_settings",
                                                "order_status_invalid",
                                                "parameter_invalid_empty",
                                                "parameter_invalid_integer",
                                                "parameter_invalid_string_blank",
                                                "parameter_invalid_string_empty",
                                                "parameter_missing",
                                                "parameter_unknown",
                                                "postal_code_invalid",
                                                "processing_error",
                                                "rate_limit",
                                                "resource_missing",
                                                "token_already_used",
                                                "invalid_request"
                                            ]
                                        },
                                        "message": {
                                            "description": "Detailed information about the error code.",
                                            "type": "string"
                                        },
                                        "decline_code": {
                                            "description": "Displays when a card issuer declines the transaction. This includes the reason for the decline if specified by the card issuer.",
                                            "type": "string"
                                        },
                                        "charge": {
                                            "description": "Displays for card-related errors. Unique identifier (ID) of the failed charge.",
                                            "type": "string"
                                        },
                                        "doc_url": {
                                            "description": "Link (URL) for more information about the reported error code.",
                                            "type": "string"
                                        },
                                        "param": {
                                            "description": "Displays for card parameter errors. The error message can inform users entering card information of a specific problem with their entry.",
                                            "type": "string"
                                        }
                                    }
                                }
                            }
                        },
                        "description": "Unexpected error"
                    }
                }
            },
            "options": {
                "tags": [
                    "TOKENS"
                ],
                "operationId": "CreateTokenOptionsHandler",
                "summary": "Pre-filght options for creating a card token",
                "x-clover-handler": "com.clover.tokenization.handler.CreateTokenOptionsHandler",
                "description": "(For cross-origin requests) Use the options endpoint for pre-flight `v1/tokens` POST requests",
                "requestBody": {
                    "content": {
                        "application/json": {
                            "encoding": {
                                "expand": {
                                    "explode": true,
                                    "style": "deepObject"
                                },
                                "items": {
                                    "explode": true,
                                    "style": "deepObject"
                                },
                                "metadata": {
                                    "explode": true,
                                    "style": "deepObject"
                                },
                                "shipping": {
                                    "explode": true,
                                    "style": "deepObject"
                                }
                            },
                            "schema": {
                                "description": "Card details, including metadata of the tokenized card.",
                                "properties": {
                                    "number": {
                                        "description": "Card number.",
                                        "type": "string"
                                    },
                                    "encrypted_pan": {
                                        "description": "Encrypted card primary account number (PAN) provided by TransArmor.",
                                        "type": "string"
                                    },
                                    "exp_month": {
                                        "description": "Card expiration month in 2-digit format-(MM).",
                                        "type": "string"
                                    },
                                    "exp_year": {
                                        "description": "Card expiration year in 2- or 4- digit format-(YYYY).",
                                        "type": "string"
                                    },
                                    "cvv": {
                                        "description": "Card verification value.",
                                        "type": "string"
                                    },
                                    "last4": {
                                        "description": "Last 4 numbers of the primary account number.",
                                        "type": "string"
                                    },
                                    "first6": {
                                        "description": "First 6 numbers of the primary account number.",
                                        "type": "string"
                                    },
                                    "country": {
                                        "description": "2-character country code.",
                                        "type": "string"
                                    },
                                    "brand": {
                                        "description": "Card brand.",
                                        "type": "string",
                                        "enum": [
                                            "VISA",
                                            "MC",
                                            "AMEX",
                                            "DISCOVER",
                                            "DINERS_CLUB",
                                            "JCB"
                                        ]
                                    },
                                    "id": {
                                        "description": "Unique identifier.",
                                        "type": "string"
                                    },
                                    "object": {
                                        "description": "Object type. Objects with the same type have the same value.",
                                        "type": "string"
                                    },
                                    "name": {
                                        "description": "Cardholder's full name.",
                                        "type": "string"
                                    },
                                    "address_line1": {
                                        "description": "Address line 1 (Street address/P.O. Box/Company name).",
                                        "type": "string"
                                    },
                                    "address_line2": {
                                        "description": "Address line 2 (Apartment/Suite/Unit/Building).",
                                        "type": "string"
                                    },
                                    "address_city": {
                                        "description": "City/District/Suburb/Town/Village.",
                                        "type": "string"
                                    },
                                    "address_state": {
                                        "description": "State/County/Province/Region.",
                                        "type": "string"
                                    },
                                    "address_zip": {
                                        "description": "ZIP or postal code.",
                                        "type": "string"
                                    },
                                    "address_country": {
                                        "description": "Billing address country, if provided.",
                                        "type": "string"
                                    },
                                    "cvc_check": {
                                        "description": "Results of the card verification code (CVC) check when a card payment is submitted to a card network for authorization. The card issuer checks the CVC against the information on file for the cardholder.",
                                        "type": "string",
                                        "enum": [
                                            "pass",
                                            "fail",
                                            "unavailable",
                                            "unchecked"
                                        ]
                                    }
                                }
                            }
                        }
                    }
                },
                "responses": {
                    "200": {
                        "description": "Successful response."
                    }
                }
            }
        },
        "/v1/tokens/{ctoken}": {
            "get": {
                "operationId": "GetToken",
                "summary": "Retrieve a token",
                "x-clover-handler": "com.clover.tokenization.handler.GetTokenHandler",
                "description": "Retrieve token for the provided unique ID",
                "parameters": [
                    {
                        "name": "ctoken",
                        "description": "Unique ID of the token to be retrieved",
                        "in": "path",
                        "required": true,
                        "schema": {
                            "maxLength": 128,
                            "type": "string"
                        },
                        "style": "simple"
                    }
                ],
                "responses": {
                    "200": {
                        "content": {
                            "application/json": {
                                "schema": {
                                    "properties": {
                                        "card": {
                                            "description": "Card details, including metadata of the tokenized card.",
                                            "properties": {
                                                "number": {
                                                    "description": "Card number.",
                                                    "type": "string"
                                                },
                                                "encrypted_pan": {
                                                    "description": "Encrypted card primary account number (PAN) provided by TransArmor.",
                                                    "type": "string"
                                                },
                                                "exp_month": {
                                                    "description": "Card expiration month in 2-digit format-(MM).",
                                                    "type": "string"
                                                },
                                                "exp_year": {
                                                    "description": "Card expiration year in 2- or 4- digit format-(YYYY).",
                                                    "type": "string"
                                                },
                                                "cvv": {
                                                    "description": "Card verification value.",
                                                    "type": "string"
                                                },
                                                "last4": {
                                                    "description": "Last 4 numbers of the primary account number.",
                                                    "type": "string"
                                                },
                                                "first6": {
                                                    "description": "First 6 numbers of the primary account number.",
                                                    "type": "string"
                                                },
                                                "country": {
                                                    "description": "2-character country code.",
                                                    "type": "string"
                                                },
                                                "brand": {
                                                    "description": "Card brand.",
                                                    "type": "string",
                                                    "enum": [
                                                        "VISA",
                                                        "MC",
                                                        "AMEX",
                                                        "DISCOVER",
                                                        "DINERS_CLUB",
                                                        "JCB"
                                                    ]
                                                },
                                                "id": {
                                                    "description": "Unique identifier.",
                                                    "type": "string"
                                                },
                                                "object": {
                                                    "description": "Object type. Objects with the same type have the same value.",
                                                    "type": "string"
                                                },
                                                "name": {
                                                    "description": "Cardholder's full name.",
                                                    "type": "string"
                                                },
                                                "address_line1": {
                                                    "description": "Address line 1 (Street address/P.O. Box/Company name).",
                                                    "type": "string"
                                                },
                                                "address_line2": {
                                                    "description": "Address line 2 (Apartment/Suite/Unit/Building).",
                                                    "type": "string"
                                                },
                                                "address_city": {
                                                    "description": "City/District/Suburb/Town/Village.",
                                                    "type": "string"
                                                },
                                                "address_state": {
                                                    "description": "State/County/Province/Region.",
                                                    "type": "string"
                                                },
                                                "address_zip": {
                                                    "description": "ZIP or postal code.",
                                                    "type": "string"
                                                },
                                                "address_country": {
                                                    "description": "Billing address country, if provided.",
                                                    "type": "string"
                                                },
                                                "cvc_check": {
                                                    "description": "Results of the card verification code (CVC) check when a card payment is submitted to a card network for authorization. The card issuer checks the CVC against the information on file for the cardholder.",
                                                    "type": "string",
                                                    "enum": [
                                                        "pass",
                                                        "fail",
                                                        "unavailable",
                                                        "unchecked"
                                                    ]
                                                }
                                            }
                                        },
                                        "cloverToken": {
                                            "properties": {
                                                "id": {
                                                    "description": "Unique ID",
                                                    "type": "string",
                                                    "maxLength": 128
                                                },
                                                "tokenValue": {
                                                    "description": "Public source token by Clover",
                                                    "type": "string"
                                                },
                                                "merchantUuid": {
                                                    "description": "Merchant UUID",
                                                    "type": "string"
                                                },
                                                "developerAppUuid": {
                                                    "description": "Developer UUID",
                                                    "type": "string"
                                                },
                                                "createdTime": {
                                                    "type": "integer"
                                                },
                                                "lastAccessedTime": {
                                                    "type": "integer"
                                                }
                                            }
                                        },
                                        "multipayToken": {
                                            "properties": {
                                                "id": {
                                                    "description": "Unique ID",
                                                    "type": "string",
                                                    "maxLength": 13
                                                },
                                                "tokenValue": {
                                                    "description": "Private HSM encrypted token value provided by TransArmor",
                                                    "type": "string"
                                                },
                                                "tokenValueBackup": {
                                                    "description": "Private RSA encrypted token value provided by TransArmor",
                                                    "type": "string"
                                                },
                                                "taTokenType": {
                                                    "description": "TransArmor token type",
                                                    "type": "string"
                                                },
                                                "createdTime": {
                                                    "type": "integer"
                                                },
                                                "modifiedTime": {
                                                    "type": "integer"
                                                }
                                            }
                                        },
                                        "tokenMeta": {
                                            "properties": {
                                                "id": {
                                                    "description": "Unique ID",
                                                    "type": "string",
                                                    "maxLength": 13
                                                },
                                                "cloverTokenId": {
                                                    "description": "Meta ID of the token stored by Clover",
                                                    "type": "integer"
                                                },
                                                "tokenStatus": {
                                                    "type": "string",
                                                    "enum": [
                                                        "NEW",
                                                        "VERIFIED"
                                                    ]
                                                },
                                                "tokenType": {
                                                    "type": "string",
                                                    "enum": [
                                                        "ONEOFF",
                                                        "MULTIPAY",
                                                        "RECURRING"
                                                    ]
                                                },
                                                "tokenProvider": {
                                                    "type": "string",
                                                    "enum": [
                                                        "TASTM",
                                                        "IPG",
                                                        "MOCK"
                                                    ]
                                                },
                                                "paymentInstrument": {
                                                    "type": "string",
                                                    "enum": [
                                                        "CARD"
                                                    ]
                                                },
                                                "createdTime": {
                                                    "type": "integer"
                                                },
                                                "modifiedTime": {
                                                    "type": "integer"
                                                }
                                            }
                                        }
                                    }
                                }
                            }
                        },
                        "description": "Successful response"
                    },
                    "default": {
                        "content": {
                            "application/json": {
                                "schema": {
                                    "description": "An error response from the API.",
                                    "properties": {
                                        "type": {
                                            "description": "Error type.",
                                            "enum": [
                                                "api_connection_error",
                                                "api_error",
                                                "authentication_error",
                                                "card_error",
                                                "idempotency_error",
                                                "invalid_request_error",
                                                "rate_limit_error",
                                                "validation_error"
                                            ]
                                        },
                                        "code": {
                                            "description": "Error codes. Additional information about the error that users can use to identify the issue.",
                                            "enum": [
                                                "amount_too_large",
                                                "amount_too_small",
                                                "api_key_expired",
                                                "card_declined",
                                                "charge_already_captured",
                                                "charge_already_refunded",
                                                "charge_disputed",
                                                "charge_exceeds_source_limit",
                                                "charge_expired_for_capture",
                                                "country_unsupported",
                                                "email_invalid",
                                                "expired_card",
                                                "incorrect_address",
                                                "incorrect_cvc",
                                                "incorrect_number",
                                                "incorrect_zip",
                                                "invalid_card_type",
                                                "invalid_charge_amount",
                                                "invalid_cvc",
                                                "invalid_expiry_month",
                                                "invalid_expiry_year",
                                                "invalid_number",
                                                "missing",
                                                "order_creation_failed",
                                                "order_required_settings",
                                                "order_status_invalid",
                                                "parameter_invalid_empty",
                                                "parameter_invalid_integer",
                                                "parameter_invalid_string_blank",
                                                "parameter_invalid_string_empty",
                                                "parameter_missing",
                                                "parameter_unknown",
                                                "postal_code_invalid",
                                                "processing_error",
                                                "rate_limit",
                                                "resource_missing",
                                                "token_already_used",
                                                "invalid_request"
                                            ]
                                        },
                                        "message": {
                                            "description": "Detailed information about the error code.",
                                            "type": "string"
                                        },
                                        "decline_code": {
                                            "description": "Displays when a card issuer declines the transaction. This includes the reason for the decline if specified by the card issuer.",
                                            "type": "string"
                                        },
                                        "charge": {
                                            "description": "Displays for card-related errors. Unique identifier (ID) of the failed charge.",
                                            "type": "string"
                                        },
                                        "doc_url": {
                                            "description": "Link (URL) for more information about the reported error code.",
                                            "type": "string"
                                        },
                                        "param": {
                                            "description": "Displays for card parameter errors. The error message can inform users entering card information of a specific problem with their entry.",
                                            "type": "string"
                                        }
                                    }
                                }
                            }
                        },
                        "description": "Error response"
                    }
                }
            },
            "put": {
                "operationId": "UpdateToken",
                "summary": "Set token as reusable or permanent",
                "x-clover-handler": "com.clover.tokenization.handler.UpdateTokenHandler",
                "description": "<p></p>",
                "parameters": [
                    {
                        "name": "ctoken",
                        "description": "Unique ID of the token to be retrieved",
                        "in": "path",
                        "required": true,
                        "schema": {
                            "maxLength": 128,
                            "type": "string"
                        },
                        "style": "simple"
                    }
                ],
                "requestBody": {
                    "content": {
                        "application/json": {
                            "encoding": {
                                "expand": {
                                    "explode": true,
                                    "style": "deepObject"
                                },
                                "items": {
                                    "explode": true,
                                    "style": "deepObject"
                                },
                                "metadata": {
                                    "explode": true,
                                    "style": "deepObject"
                                },
                                "shipping": {
                                    "explode": true,
                                    "style": "deepObject"
                                }
                            },
                            "schema": {
                                "additionalProperties": false,
                                "properties": {
                                    "token": {
                                        "description": "Public source token by Clover",
                                        "maxLength": 128,
                                        "type": "string"
                                    },
                                    "type": {
                                        "type": "string",
                                        "enum": [
                                            "ONEOFF",
                                            "MULTIPAY",
                                            "RECURRING"
                                        ]
                                    }
                                }
                            }
                        }
                    }
                },
                "responses": {
                    "200": {
                        "description": "OK"
                    },
                    "400": {
                        "content": {
                            "application/json": {
                                "schema": {
                                    "description": "An error response from the API.",
                                    "properties": {
                                        "type": {
                                            "description": "Error type.",
                                            "enum": [
                                                "api_connection_error",
                                                "api_error",
                                                "authentication_error",
                                                "card_error",
                                                "idempotency_error",
                                                "invalid_request_error",
                                                "rate_limit_error",
                                                "validation_error"
                                            ]
                                        },
                                        "code": {
                                            "description": "Error codes. Additional information about the error that users can use to identify the issue.",
                                            "enum": [
                                                "amount_too_large",
                                                "amount_too_small",
                                                "api_key_expired",
                                                "card_declined",
                                                "charge_already_captured",
                                                "charge_already_refunded",
                                                "charge_disputed",
                                                "charge_exceeds_source_limit",
                                                "charge_expired_for_capture",
                                                "country_unsupported",
                                                "email_invalid",
                                                "expired_card",
                                                "incorrect_address",
                                                "incorrect_cvc",
                                                "incorrect_number",
                                                "incorrect_zip",
                                                "invalid_card_type",
                                                "invalid_charge_amount",
                                                "invalid_cvc",
                                                "invalid_expiry_month",
                                                "invalid_expiry_year",
                                                "invalid_number",
                                                "missing",
                                                "order_creation_failed",
                                                "order_required_settings",
                                                "order_status_invalid",
                                                "parameter_invalid_empty",
                                                "parameter_invalid_integer",
                                                "parameter_invalid_string_blank",
                                                "parameter_invalid_string_empty",
                                                "parameter_missing",
                                                "parameter_unknown",
                                                "postal_code_invalid",
                                                "processing_error",
                                                "rate_limit",
                                                "resource_missing",
                                                "token_already_used",
                                                "invalid_request"
                                            ]
                                        },
                                        "message": {
                                            "description": "Detailed information about the error code.",
                                            "type": "string"
                                        },
                                        "decline_code": {
                                            "description": "Displays when a card issuer declines the transaction. This includes the reason for the decline if specified by the card issuer.",
                                            "type": "string"
                                        },
                                        "charge": {
                                            "description": "Displays for card-related errors. Unique identifier (ID) of the failed charge.",
                                            "type": "string"
                                        },
                                        "doc_url": {
                                            "description": "Link (URL) for more information about the reported error code.",
                                            "type": "string"
                                        },
                                        "param": {
                                            "description": "Displays for card parameter errors. The error message can inform users entering card information of a specific problem with their entry.",
                                            "type": "string"
                                        }
                                    }
                                }
                            }
                        },
                        "description": "Bad request"
                    },
                    "401": {
                        "content": {
                            "application/json": {
                                "schema": {
                                    "description": "An error response from the API.",
                                    "properties": {
                                        "type": {
                                            "description": "Error type.",
                                            "enum": [
                                                "api_connection_error",
                                                "api_error",
                                                "authentication_error",
                                                "card_error",
                                                "idempotency_error",
                                                "invalid_request_error",
                                                "rate_limit_error",
                                                "validation_error"
                                            ]
                                        },
                                        "code": {
                                            "description": "Error codes. Additional information about the error that users can use to identify the issue.",
                                            "enum": [
                                                "amount_too_large",
                                                "amount_too_small",
                                                "api_key_expired",
                                                "card_declined",
                                                "charge_already_captured",
                                                "charge_already_refunded",
                                                "charge_disputed",
                                                "charge_exceeds_source_limit",
                                                "charge_expired_for_capture",
                                                "country_unsupported",
                                                "email_invalid",
                                                "expired_card",
                                                "incorrect_address",
                                                "incorrect_cvc",
                                                "incorrect_number",
                                                "incorrect_zip",
                                                "invalid_card_type",
                                                "invalid_charge_amount",
                                                "invalid_cvc",
                                                "invalid_expiry_month",
                                                "invalid_expiry_year",
                                                "invalid_number",
                                                "missing",
                                                "order_creation_failed",
                                                "order_required_settings",
                                                "order_status_invalid",
                                                "parameter_invalid_empty",
                                                "parameter_invalid_integer",
                                                "parameter_invalid_string_blank",
                                                "parameter_invalid_string_empty",
                                                "parameter_missing",
                                                "parameter_unknown",
                                                "postal_code_invalid",
                                                "processing_error",
                                                "rate_limit",
                                                "resource_missing",
                                                "token_already_used",
                                                "invalid_request"
                                            ]
                                        },
                                        "message": {
                                            "description": "Detailed information about the error code.",
                                            "type": "string"
                                        },
                                        "decline_code": {
                                            "description": "Displays when a card issuer declines the transaction. This includes the reason for the decline if specified by the card issuer.",
                                            "type": "string"
                                        },
                                        "charge": {
                                            "description": "Displays for card-related errors. Unique identifier (ID) of the failed charge.",
                                            "type": "string"
                                        },
                                        "doc_url": {
                                            "description": "Link (URL) for more information about the reported error code.",
                                            "type": "string"
                                        },
                                        "param": {
                                            "description": "Displays for card parameter errors. The error message can inform users entering card information of a specific problem with their entry.",
                                            "type": "string"
                                        }
                                    }
                                }
                            }
                        },
                        "description": "Authorization information is missing or invalid."
                    },
                    "5XX": {
                        "content": {
                            "application/json": {
                                "schema": {
                                    "description": "An error response from the API.",
                                    "properties": {
                                        "type": {
                                            "description": "Error type.",
                                            "enum": [
                                                "api_connection_error",
                                                "api_error",
                                                "authentication_error",
                                                "card_error",
                                                "idempotency_error",
                                                "invalid_request_error",
                                                "rate_limit_error",
                                                "validation_error"
                                            ]
                                        },
                                        "code": {
                                            "description": "Error codes. Additional information about the error that users can use to identify the issue.",
                                            "enum": [
                                                "amount_too_large",
                                                "amount_too_small",
                                                "api_key_expired",
                                                "card_declined",
                                                "charge_already_captured",
                                                "charge_already_refunded",
                                                "charge_disputed",
                                                "charge_exceeds_source_limit",
                                                "charge_expired_for_capture",
                                                "country_unsupported",
                                                "email_invalid",
                                                "expired_card",
                                                "incorrect_address",
                                                "incorrect_cvc",
                                                "incorrect_number",
                                                "incorrect_zip",
                                                "invalid_card_type",
                                                "invalid_charge_amount",
                                                "invalid_cvc",
                                                "invalid_expiry_month",
                                                "invalid_expiry_year",
                                                "invalid_number",
                                                "missing",
                                                "order_creation_failed",
                                                "order_required_settings",
                                                "order_status_invalid",
                                                "parameter_invalid_empty",
                                                "parameter_invalid_integer",
                                                "parameter_invalid_string_blank",
                                                "parameter_invalid_string_empty",
                                                "parameter_missing",
                                                "parameter_unknown",
                                                "postal_code_invalid",
                                                "processing_error",
                                                "rate_limit",
                                                "resource_missing",
                                                "token_already_used",
                                                "invalid_request"
                                            ]
                                        },
                                        "message": {
                                            "description": "Detailed information about the error code.",
                                            "type": "string"
                                        },
                                        "decline_code": {
                                            "description": "Displays when a card issuer declines the transaction. This includes the reason for the decline if specified by the card issuer.",
                                            "type": "string"
                                        },
                                        "charge": {
                                            "description": "Displays for card-related errors. Unique identifier (ID) of the failed charge.",
                                            "type": "string"
                                        },
                                        "doc_url": {
                                            "description": "Link (URL) for more information about the reported error code.",
                                            "type": "string"
                                        },
                                        "param": {
                                            "description": "Displays for card parameter errors. The error message can inform users entering card information of a specific problem with their entry.",
                                            "type": "string"
                                        }
                                    }
                                }
                            }
                        },
                        "description": "Unexpected error"
                    }
                }
            }
        }
    },
    "x-readme": {
        "explorer-enabled": true,
        "proxy-enabled": true,
        "samples-enabled": true
    }
}
