# gitattrs

Example, using git `clean` and `smudge` filters
nb: Having played with using git clean and smudge, to protect secrets, I wouldn't recommend it, it's too easy to get it wrong... 
My preferred approach would be to use [Mozilla SOPS](https://github.com/getsops/sops) with one of the providers, AWS, GCP, Azure, etc.

Either way, it may be useful for other non-secret related use cases.

When going from staging to working directory, the clean and smudge filters would be activated against the files mentioned in the filter 
(view the filter, in the [.gitattributes](.gitattributes) file)

e.g. In this case...
```bash
*.env filter=updateApiKey
```

Run the following, to add the commands 

`(this is using local git config, could put it in global git config, if required)`
```bash
git config --local filter.updateApiKey.smudge 'sed "s/{SECURE_API_KEY}/fd716224-2881-4262-952f-7802a13ea50a/"'
git config --local filter.updateApiKey.clean 'sed "s/fd716224-2881-4262-952f-7802a13ea50a/{SECURE_API_KEY}/"'
```


<br />

---

<br />

### Git Smudge
“smudge” filter is run on checkout
<img src="git-smudge.png">



<br />

---

<br />


### Git Clean
“clean” filter is run when files are staged

<img src="git-clean.png">


### Testing
To test, create a file, e.g. x.env, with the following content
```bash
API_KEY=fd716224-2881-4262-952f-7802a13ea50a
```

When the file is staged and pushed, it should look like this
```bash
API_KEY={SECURE_API_KEY}
```


## References
https://git-scm.com/book/en/v2/Customizing-Git-Git-Attributes#_keyword_expansion
https://developers.redhat.com/articles/2022/02/02/protect-secrets-git-cleansmudge-filter
