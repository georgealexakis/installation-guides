# Installation guides

Many installation guides for miscellaneous stuff.


# Startup service for Ubuntu

1. ` cd /etc/systemd/system `
2. ` nano my_script.service `

```
No environment
[Unit]
 Description=starup_scripts_noenv
 After=network.target

[Service]
 User=george
 WorkingDirectory=/home/george
 ExecStartPre=/bin/sleep 10
 ExecStart=/usr/bin/python3 /home/george/test.py
 Restart=on-failure

[Install]
 WantedBy=multi-user.target
```

or 

With environment

```
[Unit]
Description=starup_scripts_env
After=network.target

[Service]
User=george
WorkingDirectory=/home/george
ExecStartPre=/bin/sleep 10
ExecStart=/bin/bash -c "source /home/george/venv/bin/activate && python /home/george/test.py"
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

3. ` sudo systemctl daemon-reload `
4. ` sudo systemctl start my_script.service ` or ` sudo systemctl restart my_script.service `
5. ` sudo systemctl enable my_script.service `
6. ` sudo journalctl -u my_script.service `
7. ` sudo systemctl status my_script `

# Detectron 2 Installation

https://helloshreyas.com/how-to-install-detectron2-on-windows-machine

Install Visual Studio
Make sure Desktop development with C++ is checked
Windows 11 SDK check

```
conda create --name detectron_env python=3.12

conda activate detectron_env

conda install pytorch torchvision torchaudio pytorch-cuda=12.4 -c pytorch -c nvidia

pip install Cython==0.29.33 opencv-python matplotlib==3.6.3 PyYAML protobuf==4.21.12 ninja==1.11.1

pip install "numpy<2.0"

git clone https://github.com/facebookresearch/detectron2.git

cd detectron2

python setup.py build develop

pip install -e .

python -c "import detectron2; print(detectron2.__version__)"
```

```
conda clean --all
conda remove -n ENV_NAME --all
```