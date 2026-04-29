# Layer 2 — VisualEther FXT

VisualEther FXT files for **Layer 2** (Ethernet / PPP / Frame Relay) packet captures.

## Files

- `explore.fxt.xml` — full-capture exploratory template. Renders every
  recognized packet as a labeled message in a sequence diagram, with
  protocol-specific opcodes and parameters.
- `hosts.txt` — topology-role labels for the IP addresses observed in
  the source captures (e.g. `R1 (PE)`, `R2 (RR)`). Greatly improves
  diagram readability over bare IP addresses.

## Render against your captures

```bash
visualether generate \
    --fxt explore.fxt.xml \
    --input "<your-captures>/*.pcapng" \
    --hosts-file hosts.txt \
    --output output \
    --format combined
```

`hosts.txt` was authored against captures from Nick Russo's `layer2_pcap`
collection — see the [top-level README](../README.md) for download
links. Other captures will still render; host labels just fall back to
bare IP addresses for any address not in the file.

## Pre-rendered diagrams

The rendered output of these templates against Nick's full collection is
hosted at <https://diagrams.eventhelix.com/nick-russo/>. Browse there
first if you only want to read the diagrams.
