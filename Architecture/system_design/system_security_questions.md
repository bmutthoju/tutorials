1. What is WAF?
	1. Web Application Firewall
2. How is ABAC different from RBAC? Why do we need it?
3. Why do queues need ACLs?
4. How to implement security telemetry? What golden signals are captured?
5. What is SIEM?
6. What is IDS?
7. What is IPS?
8. What information is captured in Audit logs?
9. What is SOC?
10. What is PII?
11. What is a botnet?
12. What is a supply-chain attacker?
13. What is ransomware?
14. What is spoofing?
15. What is STRIDE?
16. What is workload identity? How is it used?
17. What are passkeys?
18. How does ABAC work?
19. Where are authentication and authorization configured?
20. What is header normalization?
21. How is tenant identification implemented?
22. What is XSS?
23. What are protocol anomalies?
24. What is credential stuffing?
25. What is a scraping attack?
26. How is automated certificate rotation implemented?
27. How is identity implemented with a service mesh?
28. How is traffic policy implemented with a service mesh?
29. How is authorization implemented with a service mesh?
30. How is ABAC implemented?
31. Aren't ReBAC and RBAC the same?
32. Give examples of policy engines. How to integrate them?
33. What is Local PDP?
34. How to implement overlapping credentials?
35. How to integrate an encryption service or KMS with an application to encrypt sensitive fields and store them in the DB?
36. How is envelope encryption implemented? Give an example.
37. How is row-level security implemented in the DB?
38. How to implement database-level tenant isolation?
39. How is security implemented for Kafka?
40. What is a short-lived client URL? How is it implemented?
41. What is DNS filtering?
42. What are network policies? How to implement them?
43. How is service identity used?
44. How is RBAC implemented in K8s?
45. How is NetworkPolicy implemented in k8s?
46. How is Pod security implemented in k8s?
47. What is image scanning? How is it implemented in k8s?
48. What is Admission control? How is it implemented in k8s?
49. What is runtime security? How is it implemented in k8s?
50. How are service accounts used in k8s?
51. What is workload identity? How is it used in k8s?
52. How to configure mTLS in k8s?
53. How is audit logging implemented in k8s?
54. What is SAST?
55. What is SBOM?
56. How are the following stages implemented?

CI -> SAST -> Dependency scanning -> Container scanning -> SBOM -> Image scanning -> registry -> Admission control -> k8s

57. What is SOC?
58. How does CDN protect from DDos?
59. What is traffic scrubbing?
60. What is SYN flood?
61. What is SYN cookies?
62. How does Global DNS work?
63. What is cache poisoning?
64. What are the following and how do they work?

Content-Security-Policy
Strict-Transport-Security
X-Content-Type-Options
Referrer-Policy
Permissions-Policy

Cookie seetings:
Secure
HttpOnly
SameSite

57. What are the following and how do they work?

XSS
CSRF
CORS
Clickjacking
Token theft
Session fixation
Open redirects

58. How to set up a DB user per service in PostgreSQL?
59. How does cloud IAM work?
60. What are k8s service accounts? How are they implemented?
61. How does a global load balancer work?
62. How does a control plane define the following?

Identity
Policies
Certificates
Keys
Configuration
Roles
Permissions
Security rules

63. How does a data plan enforce the following?

Authentication
Authorization
Network policy
Traffic policy
Encryption
Rate limiting

64. How is the control-plane + data-plane architecture implemented?
65. How is a stolen JWT token handled?
66. What is failure-mode analysis?
