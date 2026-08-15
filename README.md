# OSI Rack Trainer

A drag-and-drop memory trainer for the OSI model, built for **CompTIA Network+ (N10-009), objective 1.1**.

The stack is presented as a 7U equipment rack. Layer names, PDUs, addresses and devices are "modules" you seat into units. The blacked-out cells from the standard OSI/TCP-IP comparison chart are **blanking plates** — you have to install them deliberately, because knowing where nothing goes is half the objective.

Single HTML file, no build step, no dependencies.

---

## Run it

Open `index.html` in any desktop browser. That's the whole install.

To serve it locally instead:

```bash
python3 -m http.server 8000
# http://localhost:8000
```

## Stages

Stages are hard-gated. Each one opens only when the previous is finished **clean** — zero wrong drops and zero full answer reveals.

| Stage | Name | Gate |
|---|---|---|
| 1 | Stack Builder | One clean run top-down (7→1) **and** one bottom-up (1→7) |
| 2 | Attribute Sort | Clean run on each of three columns: PDU, Address, Devices |
| 3 | Full Chart | One clean reconstruction of all six columns |
| 4 | Bins & Triage | No gate — free play |

## Hints

Each empty unit has a `?` that steps through three tiers:

1. The mnemonic word (*All People Seem To Need Data Processing* / *Apple Tainted Ingest Never* / *Drippy Sweet Pancakes For Breakfast*)
2. First letter of the answer
3. The answer itself — this one is logged and costs you the clean run

## Stage 4 content

- **Protocol bins** — 38 cards: HTTP, TLS, NetBIOS, TCP, OSPF, ARP, single-mode fiber, and so on, sorted into layer bins.
- **Fault triage** — 18 symptom cards written as tickets ("trunk port is passing the wrong VLAN tag", "ACL is dropping traffic on TCP 443"). This is the mode that actually maps to exam questions.

Accuracy per layer accumulates across every mode and every session, so the strip under the rack becomes an honest report of which layer you keep fumbling.

## Two content calls worth knowing

**ARP is scored as Layer 2.** It is often called "Layer 2.5" because it maps L3 addresses to L2 addresses, but CompTIA treats it as data link.

**DNS is scored as Layer 7.** Some older courseware places it at Layer 5 (session) because of its name-resolution role. CompTIA and Professor Messer both put it at the application layer.

## Storage

Progress persists automatically. The app uses `window.storage` when running inside a Claude artifact and falls back to `localStorage` everywhere else. "Wipe all saved progress" at the bottom of the page clears it.

## Files

```
index.html                    the entire application
docs/osi-reference.md         the chart in markdown, for quick review
.github/workflows/pages.yml   optional GitHub Pages deploy
```

## License

MIT — see [LICENSE](LICENSE).
