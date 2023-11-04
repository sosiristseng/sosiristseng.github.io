---
title: parallel
tags:
  - linux
  - command-line
---

[GNU parallel](https://www.gnu.org/software/parallel/parallel_tutorial.html) runs commands in parallel. For instance, to find all jupyter notebook files (`docs/*.ipynb`) and execute them in parallel, with 2 processes (`-j2`):

```sh
parallel -j2 jupyter nbconvert --to notebook --execute --inplace {} ::: docs/*.ipynb
```

You can set the number of parallel jobs with the `-j` flag. e.g. `-j8` runs 8 jobs in parallel.

## Display execution log

Use `--joblog <logfile>`. For example,

```sh
parallel --joblog /tmp/log -j2 jupyter nbconvert --to notebook --execute --inplace {} ::: docs/*.ipynb

cat /tmp/log
```
