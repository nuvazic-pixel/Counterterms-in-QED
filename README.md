# Bhabha QED NLO (Hybrid NLO ⊗ ISR ⊗ FSR)

Hybridized, acceptance-level Bhabha scattering at √s = 10 GeV with:
- **ISR (LL)** via Gribov–Lipatov structure functions (x₁,x₂ convolution)
- **FSR (LL)** with a **recombination cone** (photons in cone clustered into the lepton)
- **Vacuum polarization** (electron loop, OS) folded point-by-point
- A tunable **hard one-loop remainder** band `C_hard ∈ [−2%, +2%]` (boxes + soft constant) to bracket the finite NLO pieces without double-counting collinear logs

Outputs: CSVs and plots for
- SV-only vs exponentiated (soft) scans
- ISR (LL) angle scan
- ISR+FSR (LL) angle scan (θ₀=3°)
- Acceptance integration (20°–160°): ISR-only and ISR+FSR vs cone size
- **Hybrid** acceptance with VP and `C_hard` band

## Quick start

```bash
# Python 3.11+ recommended
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt

# Reproduce all CSVs/plots into ./data and ./plots
python scripts/reproduce.py
```

Artifacts will appear under `data/` and `plots/`.

## Repo layout

```
bhabha-qed-nlo/
├─ src/                # modular code (physics kernels & helpers)
├─ scripts/            # entrypoints (reproduce, quick benchmarks)
├─ data/               # CSV outputs
├─ plots/              # PNG plots
├─ .github/workflows/  # CI to regenerate & upload artifacts
├─ README.md
├─ LICENSE
├─ requirements.txt
└─ .gitignore
```

## CI (GitHub Actions)

The workflow in `.github/workflows/ci.yml`:
- sets up Python
- installs requirements
- runs `scripts/reproduce.py`
- uploads `data/` and `plots/` as build artifacts

You can extend this to deploy a GitHub Pages site for static plots.

## Physics notes

- **ISR** resums the large beam-collinear logs to all orders at LL, removing the need for an explicit soft cut.
- **FSR** uses a recombination cone of half-angle θ₀; photons in-cone are clustered into the lepton, leaving an out-of-cone suppression that decreases with larger θ₀.
- **Vacuum polarization** (e-only here) shifts normalization at the few-percent level.
- **`C_hard`** reflects the finite one-loop remainder (boxes + soft constant) after LL resummation; replace with an exact angle-dependent remainder when available.

## License

MIT — see `LICENSE`.

