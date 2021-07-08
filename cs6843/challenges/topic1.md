# Topic 1 Challenges
| URL                                                         | Notes                   | Flag                                                         |
| ----------------------------------------------------------- | ----------------------- | ------------------------------------------------------------ |
| m.staging.quoccabank.com                                    |                         | COMP6443{I_FOUND_IT_e7e964218749ecb479cdf80a7aade0a1.ejUzMTI3OTk=.uJqDlnacRvhvj+kcEI+qoQ==} |
| vault42.sandbox.quoccabank.com                              |                         | COMP6443{I_FOUND_IT_c41a76367bce74581a13ab5eeda16514.ejUzMTI3OTk=.mn3GcgKnXd0bkt3KjaWwLg==} |
| super-secret.admin.quoccabank.com                           |                         | COMP6443{I_FOUND_IT_e7e964218749ecb479cdf80a7aade0a1.ejUzMTI3OTk=.uJqDlnacRvhvj+kcEI+qoQ==} |
| vault42.sandbox.quoccabank.com                              |                         | COMP6443{I_FOUND_IT_a731277dbd3f90542e07d5eb065d3780.ejUzMTI3OTk=.uF+j1TgDvL1XOaDxDa2btg==} |
| adserver.quoccabank.com                                     |                         | COMP6443{I_FOUND_IT_a731277dbd3f90542e07d5eb065d3780.ejUzMTI3OTk=.uF+j1TgDvL1XOaDxDa2btg==} |
| mobile.quoccabank.com                                       |                         | COMP6443{DEV_TOOL_WORKS_GREAT.ejUzMTI3OTk=.5+XsdQHxmgV98dZKzuVt2Q==} |
| www-dev.quoccabank.com                                      |                         | COMP6443{I_FOUND_IT_785b4b718c9e07edc8d53cb0e0f21de0.ejUzMTI3OTk=.TbsWBfYRjEJD7pLvGFzqCQ==} |
| test.quoccabank.com                                         |                         | COMP6443{I_FOUND_IT_098f6bcd4621d373cade4e832627b4f6.ejUzMTI3OTk=.1PLCwVihE9G51K/OsYQNxQ==} |
| kb.quoccabank.com                                           | only accessible by hass |                                                              |
| dev.quoccabank.com                                          |                         | COMP6443{I_FOUND_IT_e77989ed21758e78331b20e477fc5582.ejUzMTI3OTk=.EjEGXevElOpZbjYjJhJGhg==} |
| careers.quoccabank.com                                      |                         | COMP6443{I_FOUND_IT_adf78c4508138a91472dcc053ab8eed4.ejUzMTI3OTk=.GerKB7/YqIpoIcZVfqH6Vw==} |
| www-preprod.quoccabank.com                                  |                         | COMP6443{I_FOUND_IT_927bb7e150b240f539875df667cb6c9b.ejUzMTI3OTk=.2GLW0/KS9NZT6WS36CiW6g==} |
| kb.quoccabank.com/7643dc3d-2262-4f1c-8fb9-197860946a66.html |                         | COMP6443{I_CAN_WRITE_H11P}                                   |
| wow-how-did-i-find-this-super-secret-backup.quoccabank.com  |                         | COMP6443{I_FOUND_IT_3dab7a2b34c290abde68408b70950f68.ejUzMTI3OTk=.AuJQkeWCoOdMns88jUvwHg==} |
| banking.quoccabank.com                                      |                         | COMP6443{I_FOUND_IT_6351e4efddc359eca697894df2bfd02d.ejUzMTI3OTk=.rtuIq6ND25bVK9ViXX4xQg==} |
| m.quoccabank.com                                            |                         | COMP6443{I_FOUND_IT_6f8f57715090da2632453988d9a1501b.ejUzMTI3OTk=.gnvhbTDnK7DzHgW3fPq64w==} |
| www-staging.quoccabank.com                                  |                         | COMP6443{I_FOUND_IT_fe955dc11265ad268ddafb2a5a1a82e2.ejUzMTI3OTk=.th8Hs1XdB0HgQiu0mjPxAg==} |
| www-cdn.quoccabank.com                                      |                         | COMP6443{I_FOUND_IT_927bb7e150b240f539875df667cb6c9b.ejUzMTI3OTk=.2GLW0/KS9NZT6WS36CiW6g==} |
| creditcard.quoccabank.com                                   |                         | COMP6443{I_FOUND_IT_3c92742f3c1349e9c46fe4dd5da62a98.ejUzMTI3OTk=.wtHzgudico392YETsEL9uQ==} |
|                                                             |                         |                                                              |
|                                                             |                         |                                                              |
|                                                             |                         |                                                              |
|                                                             |                         |                                                              |
|                                                             |                         |                                                              |
|                                                             |                         |                                                              |
|                                                             |                         |                                                              |
|                                                             |                         |                                                              |

```
GET /c98efc0d-5c3f-45ec-996a-2cb82d35ed26.html HTTP/1.1
Host: kb.quoccabank.com
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
Te: trailers
Connection: close
```



### Online Scanners

- https://subdomainfinder.c99.nl/
- www.nmmapper.com

### Scanners

- amass
- massdns
- sublistr

    ```bash
    sublist3r -v -d quoccabank.com -b
    ```
