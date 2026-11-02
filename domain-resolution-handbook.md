# How example.com Actually Resolves — Live Lookup Summary

Account used: HeziLiu (https://github.com/HeziLiu)

## 1) TLD layer — .com registry operator
IANA WHOIS for TLD COM (whois.verisign-grs.com):
- Organisation: VeriSign Global Registry Services (12061 Bluemont Way, Reston VA 20190, USA)
- Status: ACTIVE
- Created: 1985-01-01; Changed: 2026-03-10
- WHOIS server: whois.verisign-grs.com
- Nameservers: A.GTLD-SERVERS.NET ... M.GTLD-SERVERS.NET (13 servers)
- DS record: 19718 13 2 8acbb0cd28f41250a80a491389424d341522d946b0da0c0291f2d3d771d7805a
Conclusion: .com registry is operated by VeriSign — CONFIRMED.

## 2) Domain layer — EXAMPLE.COM (registry whois.verisign-grs.com)
- Domain Name: EXAMPLE.COM
- Registry Domain ID: 2336799_DOMAIN_COM-VRSN
- Registrar: RESERVED-Internet Assigned Numbers Authority (IANA ID 376)
- Registrar WHOIS Server: whois.iana.org; Registrar URL: http://res-dom.iana.org
- Created: 1995-08-14T04:00:00Z; Updated: 2026-08-14T08:01:43Z; Expiry: 2027-08-13T04:00:00Z
- Domain Status: clientDeleteProhibited, clientTransferProhibited, clientUpdateProhibited
- Name Server: ELLIOTT.NS.CLOUDFLARE.COM, HERA.NS.CLOUDFLARE.COM
- DNSSEC: signedDelegation
- DNSSEC DS Data: 2371 13 2 C988EC423E3880EB8DD8A46FE06CA230EE23F35B578D64E78B29C3E1C83D245A
- Whois DB last update: 2026-11-02T08:03:17Z

## 3) Network layer
- Name servers ELLIOTT.NS.CLOUDFLARE.COM and HERA.NS.CLOUDFLARE.COM are Cloudflare-operated (cloudflare.com namespace). CONFIRMED via AS13335.
- AS13335 (ARIN): ASName CLOUDFLARENET, Org Cloudflare, Inc. (OrgId CLOUD14), RegDate 2010-07-14, Updated 2017-02-17, NOC noc@cloudflare.com +1-650-319-8930. CONFIRMED.
- 1.1.1.1 (APNIC whois): inetnum 1.1.1.0 - 1.1.1.255, netname APNIC-LABS, descr "APNIC and Cloudflare DNS Resolver project / Routed globally by AS13335/Cloudflare", status ASSIGNED PORTABLE, org ORG-ARAD1-AP (APNIC Research and Development), source APNIC. Route 1.1.1.0/24 origin AS13335.
Conclusion: 1.1.1.1 is Cloudflare's anycast public resolver (joint APNIC/Cloudflare assignment) — CONFIRMED.
- a.iana-servers.net whois: Server A.IANA-SERVERS.NET, IP 199.43.135.53 (IPv4) and 2001:500:8F:0:0:0:0:53 (IPv6), Registrar CSC Corporate Domains, Inc., WHOIS whois.corporatedomains.com. b.iana-servers.net: Server B.IANA-SERVERS.NET, IP 199.43.133.53, same registrar.

## 4) Engineering layer — GitHub
- Star cloudflare/cloudflare: FAILED (PUT /user/starred/cloudflare/cloudflare -> 404 Not Found). The repo could not be starred; repo appears unresolvable via the API (repo, branches, commits, PRs, discussions, workflows, releases, tags all 404; search returns 422 "resources do not exist or you do not have permission").
- cloudflare/cloudflare latest commit: UNAVAILABLE (404 on commits API).
- Three most recently updated open PRs: UNAVAILABLE (list PRs 404; search 422).
- GitHub Discussions on cloudflare/cloudflare: UNAVAILABLE (repo not resolvable; categories and discussions 404).
- Latest CI run artifacts on cloudflare/cloudflare: UNAVAILABLE (workflows list 404; no runs to inspect).
- workers-sdk (wrangler CLI home) lighter pass:
  - Latest commit: sha ca55031d783d1c062c9d2437f3be39addab235ec, message "Version Packages (#16598)", author ANT Bot (workers-devprod), committer web-flow, date 2026-11-01T23:08:08Z. URL: https://github.com/cloudflare/workers-sdk/commit/ca55031d783d1c062c9d2437f3be39addab235ec
  - Open PRs: 210 (search is:open repo:cloudflare/workers-sdk, total_count 210, incomplete_results false).
  - Sample open PR #16642: "Bump the workerd-and-workers-types group with 2 updates", author dependabot[bot], created 2026-11-02T06:08:34Z, updated 2026-11-02T06:17:48Z, comments 3. Source/target branches not returned in the payload.

## 5) Wrap-up
All WHOIS lookups (TLD COM, example.com domain, AS13335, 1.1.1.1, a/b.iana-servers.net) returned live data. The dedicated .com TLD WHOIS initially errored but succeeded on retry with tld=COM. GitHub API access to cloudflare/cloudflare failed for all endpoints; workers-sdk data was retrievable. Username for all operations: HeziLiu.
