---
title: Router - Classic
weight: 30
---

## Transaction

### Execute Swap Operations

Multi-hop swap operations via `native_swap`, `terra_swap`, `loop` and `astroport`<br />

Case 1) The first source token is a native token (KRT => UST => mABNB)<br />

```json
{
  "execute_swap_operations":{
      "operations":[
         {
            "native_swap":{
               "offer_denom":"ukrw",
               "ask_denom":"uusd"
            }
         },
         {
            "terra_swap":{
               "offer_asset_info":{
                  "native_token":{
                     "denom":"uusd"
                  }
               },
               "ask_asset_info":{
                  "token":{
                     "contract_addr":"terra1avryzxnsn2denq7p2d7ukm6nkck9s0rz2llgnc"
                  }
               }
            }
         }
      ],
      "minimum_receive":"88000"
   }
}
```

Case 2) The first source token is a CW20 token (ANC => UST => KRT)<br />

Note: `Base64()` means that this JSON message should be encoded into Base64.<br />

```json
{
  "send": {
    "amount": "100000000",
    "contract": "terra14z80rwpd0alzj4xdtgqdmcqt9wd9xj5ffd60wp",
    "msg": Base64({
        "execute_swap_operations":{
            "operations":[
                {
                    "terra_swap":{
                        "offer_asset_info":{
                            "token":{
                                "contract_addr":"terra1747mad58h0w4y589y3sk84r5efqdev9q4r02pc"
                            }
                        },
                        "ask_asset_info":{
                            "native_token":{
                                "denom":"uusd"
                            }
                        }
                    }
                },
                {
                    "native_swap":{
                        "offer_denom":"uusd",
                        "ask_denom":"ukrw"
                    }
                }
            ],
            "minimum_receive":"121917057920"
        }
    })
  }
}
```

## Query


### Simulate Swap Operations

Query the amount of KRT that can be attained via UST by 10 mABNB<br />

```json
{
    "simulate_swap_operations":{
        "offer_amount":"10000000",
        "operations":[
            {
                "terra_swap":{
                    "offer_asset_info":{
                        "token":{
                            "contract_addr":"terra1747mad58h0w4y589y3sk84r5efqdev9q4r02pc"
                        }
                    },
                    "ask_asset_info":{
                        "native_token":{
                            "denom":"uusd"
                        }
                    }
                }
            },
            {
                "native_swap":{
                    "offer_denom":"uusd",
                    "ask_denom":"ukrw"
                }
            }
        ]
    }
}
```

### Reverse Simulate Swap Operations

Query the amount of ANC needed to get 10 LUNC via UST <br />
**Native swap is not supported.** <br />

```json
{
    "reverse_simulate_swap_operations":{
        "ask_amount":"10000000",
        "operations":[
            {
                "terra_swap":{
                    "offer_asset_info":{
                        "token":{
                            "contract_addr":"terra1747mad58h0w4y589y3sk84r5efqdev9q4r02pc"
                        }
                    },
                    "ask_asset_info":{
                        "native_token":{
                            "denom":"uusd"
                        }
                    }
                }
            },
            {
                "terra_swap":{
                    "offer_asset_info":{
                        "native_token":{
                            "denom":"uusd"
                        }
                    },
                    "ask_asset_info":{
                        "native_token":{
                            "denom":"uluna"
                        }
                    }
                }
            }
        ]
    }
}
```

# Router - Terra 2.0


## Transaction

### Execute Swap Operations

Multi-hop swap operations via `terra_swap`.<br />

Case 1) The first source token is a native token (LUNA => DELIGHT => TNT)<br />

```json
{
   "execute_swap_operations":{
      "operations":[
         {
            "terra_swap":{
               "offer_asset_info":{
                  "native_token":{
                     "denom":"uluna"
                  }
               },
               "ask_asset_info":{
                  "token":{
                     "contract_addr":"terra1cl0kw9axzpzkw58snj6cy0hfp0xp8xh9tudpw2exvzuupn3fafwqqhjc24"
                  }
               }
            }
         },
         {
            "terra_swap":{
               "offer_asset_info":{
                  "token":{
                     "contract_addr":"terra1cl0kw9axzpzkw58snj6cy0hfp0xp8xh9tudpw2exvzuupn3fafwqqhjc24"
                  }
               },
               "ask_asset_info":{
                  "token":{
                     "contract_addr":"terra1qnypzwqa03h8vqs0sxjp8hxw0xy5zfwyax26jgnl5k4lw92tjw0scdkrzm"
                  }
               }
            }
         }
      ],
      "minimum_receive":"1"
   }
}
```

Case 2) The first source token is a CW20 token (DELIGHT => LUNA => TNT)<br />

Note: `Base64()` means that this JSON message should be encoded into Base64.<br />

```json
{
  "send": {
    "amount": "100000000",
    "contract": "terra1cl0kw9axzpzkw58snj6cy0hfp0xp8xh9tudpw2exvzuupn3fafwqqhjc24",
    "msg": Base64({
        "execute_swap_operations":{
            "operations":[
                {
                    "terra_swap":{
                        "offer_asset_info":{
                            "token":{
                                "contract_addr":"terra1cl0kw9axzpzkw58snj6cy0hfp0xp8xh9tudpw2exvzuupn3fafwqqhjc24"
                            }
                        },
                        "ask_asset_info":{
                            "native_token":{
                                "denom":"uluna"
                            }
                        }
                    }
                },
                {
                    "terra_swap":{
                        "offer_asset_info":{
                            "native_token":{
                                "denom":"uluna"
                            }
                        },
                        "ask_asset_info":{
                            "token":{
                                "contract_addr":"terra1qnypzwqa03h8vqs0sxjp8hxw0xy5zfwyax26jgnl5k4lw92tjw0scdkrzm"
                            }
                        }
                    }
                }
            ],
            "minimum_receive":"1"
        }
    })
}
```

## Query

### Simulate Swap Operations

Query the amount of TNT that can be acquired via DELIGHT by offering 10 LUNA<br>

```json
{
    "simulate_swap_operations":{
        "offer_amount":"10000000",
        "operations":[
            {
                "terra_swap":{
                    "offer_asset_info":{
                        "native_token":{
                            "denom":"uluna"
                        }
                    },
                    "ask_asset_info":{
                        "token":{
                            "contract_addr":"terra1cl0kw9axzpzkw58snj6cy0hfp0xp8xh9tudpw2exvzuupn3fafwqqhjc24"
                        }
                    }
                }
            },
            {
                "terra_swap":{
                    "offer_asset_info":{
                        "token":{
                            "contract_addr":"terra1cl0kw9axzpzkw58snj6cy0hfp0xp8xh9tudpw2exvzuupn3fafwqqhjc24"
                        }
                    },
                    "ask_asset_info":{
                        "token":{
                            "contract_addr":"terra1qnypzwqa03h8vqs0sxjp8hxw0xy5zfwyax26jgnl5k4lw92tjw0scdkrzm"
                        }
                    }
                }
            }
        ]
    }
}
```
ex) [https://pisco-lcd.terra.dev/cosmwasm/wasm/v1/contract/terra1xp6xe6uwqrspumrkazdg90876ns4h78yw03vfxghhcy03yexcrcsdaqvc8/smart/ewogICAgInNpbXVsYXRlX3N3YXBfb3BlcmF0aW9ucyI6ewogICAgICAgICJvZmZlcl9hbW91bnQiOiIxMDAwMDAwMCIsCiAgICAgICAgIm9wZXJhdGlvbnMiOlsKICAgICAgICAgICAgewogICAgICAgICAgICAgICAgInRlcnJhX3N3YXAiOnsKICAgICAgICAgICAgICAgICAgICAib2ZmZXJfYXNzZXRfaW5mbyI6ewogICAgICAgICAgICAgICAgICAgICAgICAibmF0aXZlX3Rva2VuIjp7CiAgICAgICAgICAgICAgICAgICAgICAgICAgICAiZGVub20iOiJ1bHVuYSIKICAgICAgICAgICAgICAgICAgICAgICAgfQogICAgICAgICAgICAgICAgICAgIH0sCiAgICAgICAgICAgICAgICAgICAgImFza19hc3NldF9pbmZvIjp7CiAgICAgICAgICAgICAgICAgICAgICAgICJ0b2tlbiI6ewogICAgICAgICAgICAgICAgICAgICAgICAgICAgImNvbnRyYWN0X2FkZHIiOiJ0ZXJyYTFjbDBrdzlheHpwemt3NThzbmo2Y3kwaGZwMHhwOHhoOXR1ZHB3MmV4dnp1dXBuM2ZhZndxcWhqYzI0IgogICAgICAgICAgICAgICAgICAgICAgICB9CiAgICAgICAgICAgICAgICAgICAgfQogICAgICAgICAgICAgICAgfQogICAgICAgICAgICB9LAogICAgICAgICAgICB7CiAgICAgICAgICAgICAgICAidGVycmFfc3dhcCI6ewogICAgICAgICAgICAgICAgICAgICJvZmZlcl9hc3NldF9pbmZvIjp7CiAgICAgICAgICAgICAgICAgICAgICAgICJ0b2tlbiI6ewogICAgICAgICAgICAgICAgICAgICAgICAgICAgImNvbnRyYWN0X2FkZHIiOiJ0ZXJyYTFjbDBrdzlheHpwemt3NThzbmo2Y3kwaGZwMHhwOHhoOXR1ZHB3MmV4dnp1dXBuM2ZhZndxcWhqYzI0IgogICAgICAgICAgICAgICAgICAgICAgICB9CiAgICAgICAgICAgICAgICAgICAgfSwKICAgICAgICAgICAgICAgICAgICAiYXNrX2Fzc2V0X2luZm8iOnsKICAgICAgICAgICAgICAgICAgICAgICAgInRva2VuIjp7CiAgICAgICAgICAgICAgICAgICAgICAgICAgICAiY29udHJhY3RfYWRkciI6InRlcnJhMXFueXB6d3FhMDNoOHZxczBzeGpwOGh4dzB4eTV6Znd5YXgyNmpnbmw1azRsdzkydGp3MHNjZGtyem0iCiAgICAgICAgICAgICAgICAgICAgICAgIH0KICAgICAgICAgICAgICAgICAgICB9CiAgICAgICAgICAgICAgICB9CiAgICAgICAgICAgIH0KICAgICAgICBdCiAgICB9Cn0=](https://pisco-lcd.terra.dev/cosmwasm/wasm/v1/contract/terra1xp6xe6uwqrspumrkazdg90876ns4h78yw03vfxghhcy03yexcrcsdaqvc8/smart/ewogICAgInNpbXVsYXRlX3N3YXBfb3BlcmF0aW9ucyI6ewogICAgICAgICJvZmZlcl9hbW91bnQiOiIxMDAwMDAwMCIsCiAgICAgICAgIm9wZXJhdGlvbnMiOlsKICAgICAgICAgICAgewogICAgICAgICAgICAgICAgInRlcnJhX3N3YXAiOnsKICAgICAgICAgICAgICAgICAgICAib2ZmZXJfYXNzZXRfaW5mbyI6ewogICAgICAgICAgICAgICAgICAgICAgICAibmF0aXZlX3Rva2VuIjp7CiAgICAgICAgICAgICAgICAgICAgICAgICAgICAiZGVub20iOiJ1bHVuYSIKICAgICAgICAgICAgICAgICAgICAgICAgfQogICAgICAgICAgICAgICAgICAgIH0sCiAgICAgICAgICAgICAgICAgICAgImFza19hc3NldF9pbmZvIjp7CiAgICAgICAgICAgICAgICAgICAgICAgICJ0b2tlbiI6ewogICAgICAgICAgICAgICAgICAgICAgICAgICAgImNvbnRyYWN0X2FkZHIiOiJ0ZXJyYTFjbDBrdzlheHpwemt3NThzbmo2Y3kwaGZwMHhwOHhoOXR1ZHB3MmV4dnp1dXBuM2ZhZndxcWhqYzI0IgogICAgICAgICAgICAgICAgICAgICAgICB9CiAgICAgICAgICAgICAgICAgICAgfQogICAgICAgICAgICAgICAgfQogICAgICAgICAgICB9LAogICAgICAgICAgICB7CiAgICAgICAgICAgICAgICAidGVycmFfc3dhcCI6ewogICAgICAgICAgICAgICAgICAgICJvZmZlcl9hc3NldF9pbmZvIjp7CiAgICAgICAgICAgICAgICAgICAgICAgICJ0b2tlbiI6ewogICAgICAgICAgICAgICAgICAgICAgICAgICAgImNvbnRyYWN0X2FkZHIiOiJ0ZXJyYTFjbDBrdzlheHpwemt3NThzbmo2Y3kwaGZwMHhwOHhoOXR1ZHB3MmV4dnp1dXBuM2ZhZndxcWhqYzI0IgogICAgICAgICAgICAgICAgICAgICAgICB9CiAgICAgICAgICAgICAgICAgICAgfSwKICAgICAgICAgICAgICAgICAgICAiYXNrX2Fzc2V0X2luZm8iOnsKICAgICAgICAgICAgICAgICAgICAgICAgInRva2VuIjp7CiAgICAgICAgICAgICAgICAgICAgICAgICAgICAiY29udHJhY3RfYWRkciI6InRlcnJhMXFueXB6d3FhMDNoOHZxczBzeGpwOGh4dzB4eTV6Znd5YXgyNmpnbmw1azRsdzkydGp3MHNjZGtyem0iCiAgICAgICAgICAgICAgICAgICAgICAgIH0KICAgICAgICAgICAgICAgICAgICB9CiAgICAgICAgICAgICAgICB9CiAgICAgICAgICAgIH0KICAgICAgICBdCiAgICB9Cn0=)

### Reverse Simulate Swap Operations

Query the amount of LUNA required to receive 10 TNT via DELIGHT<br>

```json
{
    "reverse_simulate_swap_operations":{
        "ask_amount":"10000000",
        "operations":[
            {
                "terra_swap":{
                    "offer_asset_info":{
                        "native_token":{
                            "denom":"uluna"
                        }
                    },
                    "ask_asset_info":{
                        "token":{
                            "contract_addr":"terra1cl0kw9axzpzkw58snj6cy0hfp0xp8xh9tudpw2exvzuupn3fafwqqhjc24"
                        }
                    }
                }
            },
            {
                "terra_swap":{
                    "offer_asset_info":{
                        "token":{
                            "contract_addr":"terra1cl0kw9axzpzkw58snj6cy0hfp0xp8xh9tudpw2exvzuupn3fafwqqhjc24"
                        }
                    },
                    "ask_asset_info":{
                        "token":{
                            "contract_addr":"terra1qnypzwqa03h8vqs0sxjp8hxw0xy5zfwyax26jgnl5k4lw92tjw0scdkrzm"
                        }
                    }
                }
            }
        ]
    }
}
```
