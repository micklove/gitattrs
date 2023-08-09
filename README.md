# gitattrs

Example, using git `clean` and `smudge` filters

When going from staging to working directory, the clean and smudge filters would be activated against the files mentioned in the filter (in the .gitattributes file)


```bash
git config --local filter.updateApiKey.smudge 'sed "s/{SECURE_API_KEY}/fd716224-2881-4262-952f-7802a13ea50a/" && echo smudge'
git config --local filter.updateApiKey.clean 'sed "s/fd716224-2881-4262-952f-7802a13ea50a/{SECURE_API_KEY}/" && echo clean'
```
