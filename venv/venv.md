## Virtual Environments 

- A *virtual environment* is a space to install packages which belong to a certain project
  
## How to 

- Create virtual environment
- It is common to create the virtual environment within the project folder
- Do **not** save any other files within the directory *env_name*
- Include the directory *env_name* in *.gitignore*
```bash
python3 -m venv env_name
```


- Activate virtual environment
```bash
source -m env_name/bin/activate
```

- Deactivate virtual environment
```bash
deactivate
```

- Delete virtual environment
```bash
rm -rf path/to/env_name
```

- Check all installed packages
```bash
pip list
```

- Create a list of all packages in current virtual environment
```bash
pip freeze > requirments.txt
```

- Create a virutal enviroment which includes all system packages
```bash
python3 -m venv env_name --system-site-packages
```