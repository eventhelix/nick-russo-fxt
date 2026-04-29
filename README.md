# Nick Russo PCAP — VisualEther FXT Files

This repository contains **FXT files** ([Field Extraction Templates](https://www.eventhelix.com/visualether/)) for use with [VisualEther](https://www.eventhelix.com/visualether/) — a tool that turns Wireshark packet captures into protocol sequence diagrams.

The templates are designed to be used against the late **[Nick Russo](https://www.eventhelix.com/visualether/)**'s comprehensive packet-capture collection, covering 41 protocol families across routing, switching, IP services, MPLS, tunneling, multicast, management, applications, collaboration, IoT/wireless, and SDN.

## See the rendered diagrams first

Before downloading anything, you can browse the diagrams these templates produce — fully rendered, interactive, hosted by EventHelix:

**→ <https://diagrams.eventhelix.com/nick-russo/>**

That site is regenerated from this repository's templates plus Nick's pcaps. If you only want to *read* the diagrams, the hosted site is the easier path.

## Re-rendering the diagrams locally

If you want to run the templates yourself — to tweak labels, add captures, or experiment — you'll need three things:

### 1. The pcap files

Nick's site (`njrusmc.net`) is no longer reachable. The captures survive in two public archives:

- **<https://github.com/kaelemc/NickRussoContent>** — community archive, organized as zipped per-protocol bundles (e.g. `bgp_pcap.zip`).
- **[Wayback Machine snapshot](https://web.archive.org/web/20240502155743/https://njrusmc.net/jobaid/jobaid.html)** — last reachable copy of the original page.

> Nick's original "personal use only, no redistribution" clause continues to govern the source pcaps regardless of where they're obtained. Use them for personal study, troubleshooting, and education.

### 2. VisualEther

Free Community Edition: <https://www.eventhelix.com/visualether/>

Community Edition renders PDF sequence diagrams. Professional Edition adds interactive HTML viewers, per-session flow diagrams, and NDJSON structured output.

### 3. The FXT files (this repo)

Each `<protocol>_pcap/` directory contains:

- `explore.fxt.xml` — full-capture exploratory FXT. Renders every
  recognized packet as a labeled message in a sequence diagram.
- `hosts.txt` — IP → topology-role mapping (e.g. `R1 (PE)`, `R2 (RR)`)
  authored against the matching capture set in Nick's collection.
- `README.md` — what the family covers and how to render it.

### Quick start

```bash
# 1. Download the FXT templates (this repo).
git clone https://github.com/eventhelix/nick-russo-fxt.git
cd nick-russo-fxt

# 2. Drop the matching pcap zip from the community archive into the
#    corresponding directory and unzip it. For example:
#       bgp_pcap.zip → bgp_pcap/*.pcapng
unzip ../bgp_pcap.zip -d bgp_pcap/

# 3. Render with VisualEther.
visualether generate \
    --fxt bgp_pcap/explore.fxt.xml \
    --input "bgp_pcap/*.pcapng" \
    --output output/bgp_pcap \
    --hosts-file bgp_pcap/hosts.txt \
    --format combined

# 4. Open the resulting HTML/PDF.
```

For a script that batches all 41 families with the right options per protocol, see EventHelix's private companion repo (the same script that produces <https://diagrams.eventhelix.com/nick-russo/>).

## Protocol families

41 directories. See each subdirectory's `README.md` for protocol-specific notes.

**Routing**: BGP, OSPF, EIGRP, IS-IS, RIP, Babel, PIM/MSDP, Segment Routing
**Switching & Layer 2**: STP, Ethernet OAM, Layer 2 (PPP/PPPoE/FR), Non-IP, Legacy
**First Hop & Multicast**: FHRP (HSRP/VRRP/GLBP), IGMP/MLD, BFD
**Tunneling & VPN**: GRE/DMVPN/LISP, L2TP/VXLAN/OTV, IPsec/MACsec, IPv6 transition, MPLS
**Services & Management**: DHCP/DNS/SNMP/NTP, AAA, NAT, NetFlow, QoS, ICMP, IP SLA, gRPC/gNMI, RESTCONF, OpenFlow, Meraki
**Applications**: HTTP/2/3/QUIC, FTP/SFTP/TFTP, Email, Database, IoT, Storage, SIP/RTP/SCCP/MGCP/H.323
**Wireless**: 802.11, CAPWAP

## Contributing

Pull requests are welcome — better opcode labels, richer parameter extraction, clearer host-role mappings, fixes for misleading rendering. See the per-protocol READMEs for the kinds of refinements that matter most for each family.

When opening a PR, please also describe which capture(s) you tested against so reviewers can spot-check the rendered output.

## About Nick Russo

Nick Russo (1989–2024) was a CCIE-certified network engineer and educator who described his packet captures as "job aids" — references to help individuals in their daily work and technical studies:

> *Packet captures help reveal the ground truth. Use these PCAPs as references when troubleshooting complex issues.*

This repository, and the rendered diagrams at <https://diagrams.eventhelix.com/nick-russo/>, are a continuation of his teaching: the same captures, turned into searchable visual flows that make protocol behavior obvious at a glance.

More of Nick's work survives at:

- <https://github.com/nickrusso42518>
- <https://github.com/kaelemc/NickRussoContent>

## License

The FXT templates, hosts files, and per-protocol READMEs in this repository are © **EventHelix.com Inc.**, made available for use with VisualEther.

Nick Russo's pcap files (referenced but not redistributed here) remain governed by his original copyright and personal-use terms.
