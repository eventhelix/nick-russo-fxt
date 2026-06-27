# Nick Russo PCAP — VisualEther FXT Files

## In memory of Nick Russo (1985–2024)

[Nicholas "Nick" Russo](https://github.com/nickrusso42518) (December 20, 1985 – June 10, 2024) was a **CCDE (#20160041)** and **CCIE (#42518)** network engineer and one of the most prolific networking educators of his generation — an internationally recognized expert in IP/MPLS networking and design. A 2008 Computer Science graduate of the Rochester Institute of Technology, he authored books and podcasts, recorded a deep catalog of Pluralsight courses spanning BGP, OSPF, MPLS, IPsec, automation, and the CCIE/CCNP curricula, contributed open-source automation tooling, and ran [njrusmc.net](https://njrusmc.net/) as a free public reference for engineers studying and troubleshooting in the field. The community remembers him as "a bright light in network engineering."

Nick described his packet captures as *"job aids"* — references that answer questions like *"what does an OSPF adjacency actually look like on the wire?"*:

> *Packet captures help reveal the ground truth. Use these PCAPs as references when troubleshooting complex issues.*
> — Nick Russo

**This repository is a derivative of Nick's work.** The FXT templates here exist only to turn his capture collection into searchable visual sequence diagrams — the same captures, continuing his teaching. The fully rendered, interactive diagrams are hosted at **<https://diagrams.eventhelix.com/nick-russo/>**.

Explore more of Nick's work:

- [github.com/nickrusso42518](https://github.com/nickrusso42518) — his labs, automation tooling, and CCIE/CCNP study material
- In Memoriam: [Cisco Learning Network](https://learningnetwork.cisco.com/s/question/0D56e0000DuvttBCQQ/nick-russo-in-memoriamdecember-20-1985-june-10-2024) · [NANOG](https://nanog.org/resources/memoriam/memoriam-russo/)

---

## What's in this repository

This repository contains **FXT files** ([Field Extraction Templates](https://www.eventhelix.com/visualether/)) for use with [VisualEther](https://www.eventhelix.com/visualether/) — a tool that turns Wireshark packet captures into protocol sequence diagrams. The templates render Nick Russo's comprehensive packet-capture collection, covering 41 protocol families across routing, switching, IP services, MPLS, tunneling, multicast, management, applications, collaboration, IoT/wireless, and SDN.

## See the rendered diagrams first

Before downloading anything, you can browse the diagrams these templates produce — fully rendered, interactive, hosted by EventHelix:

**→ <https://diagrams.eventhelix.com/nick-russo/>**

That site is regenerated from this repository's templates plus Nick's pcaps. If you only want to *read* the diagrams, the hosted site is the easier path.

## Re-rendering the diagrams locally

If you want to run the templates yourself — to tweak labels, add captures, or experiment — you'll need three things:

### 1. The pcap files

Nick's site (`njrusmc.net`) is no longer reachable. His original job-aid page — where he published the captures himself, under his own terms — survives on the Internet Archive:

- **[Wayback Machine snapshot of `njrusmc.net/jobaid`](https://web.archive.org/web/20240719051541/https://njrusmc.net/jobaid/jobaid.html)**

> Nick marked these captures **"personal use only, no redistribution."** Please honor that: download them from his own archived page above (not third-party mirrors), and use them for personal study, troubleshooting, and education.

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

# 2. Download the matching captures from Nick's archived job-aid page
#    (Wayback Machine, linked above) and place the .pcap/.pcapng files
#    into the matching directory, e.g. bgp_pcap/.
```

**3. Render with VisualEther:**

```bash
visualether generate \
    --fxt bgp_pcap/explore.fxt.xml \
    --input "bgp_pcap/*.pcapng" \
    --output output/bgp_pcap \
    --hosts-file bgp_pcap/hosts.txt
```

VisualEther picks the output for your edition automatically: the free **Community Edition** renders a **PDF** sequence diagram, while **Professional Trial, Professional, and Server** render the interactive **combined** HTML + PDF viewer.

**4.** Open the resulting PDF — or, on Professional/Server, the HTML viewer.

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

When opening a PR, please describe which capture(s) you tested against (pull them from Nick's archived job-aid page on the Wayback Machine) so reviewers can spot-check the rendered output.

## License

The files **in this repository** — the `explore.fxt.xml` templates, `hosts.txt` files, and per-protocol READMEs, all authored by EventHelix.com Inc. — are released under the [MIT License](LICENSE).

The license applies **only to the files shared in this repository.** It does **not** cover Nick Russo's packet captures: those are not included or redistributed here and remain governed by his original copyright and "personal use only, no redistribution" terms.
