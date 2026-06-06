# DevOps Troubleshooting Log

## AWS

| ID      | Date       | Issue                         | Root Cause                                                    | Resolution                               | Lesson Learned                             |
| ------- | ---------- | ----------------------------- | ------------------------------------------------------------- | ---------------------------------------- | ------------------------------------------ |
| AWS-001 | 2026-06-06 | Permission denied (publickey) | Wrong PEM filename used (`my-key.pem` instead of `MICAH.pem`) | Used correct PEM file in SSH command     | Verify PEM filename before troubleshooting |
| AWS-002 | 2026-06-06 | Wrong SSH username            | Used incorrect login username                                 | Used `ubuntu` username                   | Different AMIs use different usernames     |
| AWS-003 | 2026-06-06 | SSH Connection timed out      | Network connectivity issue                                    | Check Port 22, Security Group, Public IP | Timeout = Network Issue                    |
| AWS-004 | 2026-06-06 | Port 22 blocked               | Security Group missing SSH rule                               | Added inbound TCP 22 rule                | First check Security Group for SSH issues  |
| AWS-005 | 2026-06-06 | Missing Public IP             | Instance not internet reachable                               | Assign/verify Public IPv4                | Public IP required for internet SSH        |

---

## Linux

| ID      | Date       | Issue                        | Root Cause                     | Resolution                  | Lesson Learned                           |
| ------- | ---------- | ---------------------------- | ------------------------------ | --------------------------- | ---------------------------------------- |
| LNX-001 | 2026-06-06 | Identity file not accessible | Wrong filename/path            | Used correct PEM file       | Read terminal warnings carefully         |
| LNX-002 | 2026-06-06 | Incorrect PEM permissions    | Permissions not restricted     | `chmod 400 MICAH.pem`       | PEM files should be read-only for owner  |
| LNX-003 | 2026-06-06 | Stuck at `(END)` screen      | Inside `less` pager            | Press `q`                   | `(END)` means pager, not frozen terminal |
| LNX-004 | 2026-06-06 | Understanding `ls -l` output | Needed permission verification | Used `ls -l MICAH.pem`      | Verify permissions before SSH            |
| LNX-005 | 2026-06-06 | Understanding `chmod 400`    | SSH key security requirement   | Applied correct permissions | Owner read-only access                   |

---

## Nginx

| ID      | Date       | Issue                               | Root Cause                          | Resolution                   | Lesson Learned                                  |
| ------- | ---------- | ----------------------------------- | ----------------------------------- | ---------------------------- | ----------------------------------------------- |
| NGX-001 | 2026-06-06 | Site not accessible after install   | Service/Network verification needed | Check Nginx status first     | Service → Port → Network                        |
| NGX-002 | 2026-06-06 | Nginx running but site inaccessible | Port 80 not open                    | Allow HTTP in Security Group | Running service doesn't guarantee accessibility |
