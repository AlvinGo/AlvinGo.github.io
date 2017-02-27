---
title: Jupyter 安装python kernel
---

## Jupyter安装python2/3 kernel

- Python3里安装Python2 Kernel

```bash
python2 -m pip install ipykernel
python2 -m ipykernel install --user
```

- Python2里安装Python3 Kernel

把上面的python2 换成 python3就可以了。

```bash
python3 -m pip install ipykernel
python3 -m ipykernel install --user
```

详细信息请参考[官方文档](https://ipython.readthedocs.io/en/latest/install/kernel_install.html)