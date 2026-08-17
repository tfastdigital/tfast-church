# Tfast Church — church management

**Status:** Proposed — awaiting build approval
**Built on:** ChurchCRM (MIT)
**Repository:** https://github.com/tfastdigital/tfast-church
**GitHub tags:** `church-management`, `crm`, `giving`, `uganda`, `sms`, `mobile-money`, `open-source`

## The business case

Ugandan churches — Pentecostal, Anglican, Catholic parishes and the thousands of born-again fellowships — manage people, not products. Membership lists, fellowship groups, attendance, pledges, tithes and offerings. The giving part is where mobile money changes everything: members increasingly want to give by MoMo instead of carrying cash envelopes, and treasurers want a clean record they can show the finance committee.

ChurchCRM covers the people side well (families, groups, events, giving records). We add the Ugandan layer: MoMo giving with automatic recording, bulk SMS in local languages, and a member app. Churches are loyal clients — once a treasurer's records live in the system, they do not leave.

## Who buys it

- Large Pentecostal and born-again churches (500–10,000 members)
- Anglican parishes and Catholic dioceses
- Fellowship networks with multiple branches
- Church-founded schools and projects that share membership data

## How we make money

- One-time setup fee
- Monthly support contract
- Monthly hosting fee
- MoMo giving setup: one-time fee per mobile money merchant code
- Training for secretaries and treasurers

## Features in detail

### Admin (secretary / IT)

- Family and member records: photos, contact details, baptism/marriage dates, groups
- Groups and fellowships with leaders and meeting schedules
- Events calendar with attendance tracking
- Giving records: tithes, offerings, pledges, per-member statements
- MoMo giving channel with automatic ledger entries
- SMS campaigns to groups, zones or the whole church
- Report pack for the finance committee: giving trends, attendance, member growth

### Staff and leaders

- Pastors: reports, member notes, follow-up lists
- Treasurers: giving records, reconciliation, statements
- Group leaders: own group roster, attendance, communication

### Member

- Update own contact details
- Give via MoMo from the app; statement of own giving for tax/pledge purposes
- See event announcements

### Roles and permissions

| Role | What they can do |
|---|---|
| Admin | Everything, including finance reports and SMS credits |
| Pastor | Reports, member notes; no finance changes |
| Treasurer | Giving records, reconciliation, member statements |
| Group leader | Own group only: roster, attendance, messages |
| Member | Own profile, own giving statement |

## Architecture

ChurchCRM is a PHP/MySQL application — simple to host and simple to extend. The MoMo giving webhook writes straight into the giving ledger, which is the one integration that makes the product real.

- **Core:** ChurchCRM (PHP, MySQL)
- **Giving:** MoMo merchant webhook + reconciliation script
- **SMS:** shared gateway module with per-church balance
- **Member app:** Flutter, phase 2

## Languages and stack

- PHP — the core; easy to maintain and the cheapest thing to host
- MySQL/MariaDB — member data
- Node.js snippet or PHP webhook for MoMo callbacks (reuses the shared payment knowledge)
- Flutter for the member app later

## Hosting

Cloud VPS — members must be able to give from anywhere, so the webhook endpoint needs to be public. Smaller churches get a shared-hosting tier; large ones get a dedicated instance.

## Mobile app

Phase 2, yes — a Flutter member app: give, see announcements, update details. The web portal already works on phones for v1, so the app is a refinement, not a blocker.

## Versions

- **v1.0:** membership, groups, events, giving records, MoMo giving, SMS
- **v1.5:** member app, pledge campaigns with progress bars
- **v2.0:** multi-branch network dashboard, livestream/event registration

## Timeframe

8–10 weeks with 2 developers. ChurchCRM is mature, so the work is branding, the MoMo ledger integration and the training materials.

## License and rules

ChurchCRM is MIT — the easiest license to work with. Proper fork, license file intact, upstream credited in the footer. Our MoMo module and themes are our own MIT code.
