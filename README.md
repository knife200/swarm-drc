# SWARM DRC

Linux x86-64 with an NVIDIA GPU and `xz`.
Includes 8 rule decks and 6 GDS benchmarks.

Run all benchmarks:

```sh
xz -dk inputs/*.gds.xz
chmod +x swarm-drc
mkdir -p out
for layout in inputs/*.gds; do
  design=$(basename "$layout" .gds)
  for deck in rules/*.rules; do
    rule=$(basename "$deck" .rules)
    ./swarm-drc --gds "$layout" --top-cell "$design" --rules "$deck" \
      --output "out/$design.$rule.jsonl" --stats "out/$design.$rule.stats.json"
  done
done
```
