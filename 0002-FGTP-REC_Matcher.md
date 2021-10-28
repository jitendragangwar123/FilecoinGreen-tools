---
FGTP: "0002"
title: REC Matcher
status: Idea
original author: redransil
created: 2021-10-28
---

## Title
REC Matcher

## Abstract
We need to be able to algorithmically determine whether renewable energy credits (RECs) match energy consumption. One component of this is determining whether consumption and production are close enough to each other on the grid. This is currently done in the industry manually by accounting firms.

## Authors
*Feel free to add your name if you make contributions beyond fixing typos or formatting*

redransil

## Status
Idea

## What is the goal
Given a consumption location and generation location, tell whether they are in the same bidding zone.

## What are the inputs
1. Consumption location may be address, GPS, city, county or zip code where a minerID is located.
  * If a minerID is distributed, say it seals in one location and stores in another, this may not exactly map to a minerID
  * One way to do this is [minerID -> IP](https://observablehq.com/@jimpick/provider-quest-multiaddr-ip-tool) and [IP -> location](https://observablehq.com/@jimpick/provider-quest-storage-provider-to-region-mapper?collection=@jimpick/provider-quest). We are developing a methodology separately to validate this info with other data (for example, power bills) but IP is probably a good starting point.
  * What location info should we store to facilitate this?
2. Location information from a REC certificate
  * You can find them linked from [Filrep](https://filrep.io/?columns=energy&order=desc&sortBy=energy)
  * [Example I-REC](https://zero.energyweb.org/api/files/fcfa61f7-3d29-4c45-99d2-b3ce03c5d10e)
  * [Example Green-e REC](https://zero.energyweb.org/api/files/b686115d-8826-46e0-8b9e-58fb3255f743)
  * [Example GO 1](https://zero.energyweb.org/api/files/66ce7da9-4d28-46ae-a001-f57f4f5d47da)
  * [Example GO 2, Norway](https://zero.energyweb.org/api/files/1a2685ac-cc7e-4039-8a72-536c8704d795)
  * What location data should we store along with REC purchases to facilitate this?
  * In the near-term, we are expecting to have REC location and amount be available at an EWF endpoint, for example [here for f01234](https://zero.energyweb.org/api/partners/filecoin/nodes/f01234/transactions)
3. Spatial resolution
  *  The goal here is to make sure that the generation and consumption are on the same power grid. No good across-the-board standard exists for this right now
  *  One easy solution is political boundaries: ie country (if the country is reasonably small) or state/province 
  *  Another solution is to do it by either [grid interconnection](https://www.eia.gov/todayinenergy/detail.php?id=27152) or [system operator / balancing authority](https://www.ferc.gov/sites/default/files/2020-05/elec-ovr-rto-map.pdf) ie the organization that operates the power grid.
  *  The best solution would look similar to [European bidding zones](https://eepublicdownloads.entsoe.eu/clean-documents/events/2018/BZ_report/20181015_BZ_TR_FINAL.pdf) which are intended to reflect physical electric transmission constraints.
  *  This configuration may need to be updated over time

## What are the outputs
True / False whether the consumption and generation match

## Proposed Solution
*If you're interested in tackling this, please propose something!*

## Implementations and Artifacts 
No implementations

## Relevant Background
See inputs above