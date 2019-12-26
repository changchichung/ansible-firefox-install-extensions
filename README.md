# ansible-firefox-install-extensions

###prepare xpi files

* install all extension you wanted in a fresh install firefox
* create ext.tgz by this command
```
tar zxvf ext.tgz ~/.mozilla/firefox/5s17akow.default/extension*
```
* replace "5s17akow.default" to your default firefox profile name
* copy ext.tgz to roles/firefox/files/

* 先在一台乾淨的電腦上安裝firefox 以及想要使用的extension
* 使用以下指令建立一個 ext.tgz 的檔案
```
tar zxvf ext.tgz ~/.mozilla/firefox/5s17akow.default/extension*
```
* 記得把 "5s17akow.default" 換成你真正的firefox profile 目錄名稱
* 把ext.tgz 複製到 roles/firefox/files/

--- 

###modify hosts

* modify hosts to fit your environment
* records in hosts must with ssh_args ForwardAgent

* 依照環境修改 hosts 檔案
* hosts 裡面必須要有 ssh_args ForwardAgent

###run playbook to deploy

```
ansible-playbook -i hosts playbook.yml
```
---

###ansible log

```
$ ansible-playbook -i hosts firefox.yml

PLAY [all] ***********************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************
Thursday 26 December 2019  12:25:53 +0800 (0:00:00.095)       0:00:00.095 *****
ok: [hqdc075]

TASK [firefox : install firefox and languages] ***********************************************************************************
Thursday 26 December 2019  12:25:57 +0800 (0:00:03.338)       0:00:03.433 *****
[WARNING]: Could not find aptitude. Using apt-get instead

ok: [hqdc075]

TASK [firefox : run firefox to create default profile] ***************************************************************************
Thursday 26 December 2019  12:25:58 +0800 (0:00:01.557)       0:00:04.990 *****
changed: [hqdc075]

TASK [firefox : get firefox default profile name] ********************************************************************************
Thursday 26 December 2019  12:26:00 +0800 (0:00:01.420)       0:00:06.410 *****
changed: [hqdc075]

TASK [firefox : debug profile_name] **********************************************************************************************
Thursday 26 December 2019  12:26:00 +0800 (0:00:00.310)       0:00:06.721 *****
ok: [hqdc075] => {
    "profile_name": {
        "changed": true,
        "cmd": "cat ~/.mozilla/firefox/installs.ini|grep Default|cut -d = -f 2-",
        "delta": "0:00:00.003312",
        "end": "2019-12-26 12:26:00.468398",
        "failed": false,
        "rc": 0,
        "start": "2019-12-26 12:26:00.465086",
        "stderr": "",
        "stderr_lines": [],
        "stdout": "7doibipg.default-release",
        "stdout_lines": [
            "7doibipg.default-release"
        ]
    }
}

TASK [firefox : send firefox extension config] ***********************************************************************************
Thursday 26 December 2019  12:26:00 +0800 (0:00:00.073)       0:00:06.794 *****
ok: [hqdc075]

TASK [firefox : unarchive ext.tgz to user profile] *******************************************************************************
Thursday 26 December 2019  12:26:01 +0800 (0:00:01.193)       0:00:07.988 *****
changed: [hqdc075]

PLAY RECAP ***********************************************************************************************************************
hqdc075                    : ok=7    changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

Thursday 26 December 2019  12:26:02 +0800 (0:00:00.939)       0:00:08.928 *****
===============================================================================
Gathering Facts ----------------------------------------------------------------------------------------------------------- 3.34s
firefox : install firefox and languages ----------------------------------------------------------------------------------- 1.56s
firefox : run firefox to create default profile --------------------------------------------------------------------------- 1.42s
firefox : send firefox extension config ----------------------------------------------------------------------------------- 1.19s
firefox : unarchive ext.tgz to user profile ------------------------------------------------------------------------------- 0.94s
firefox : get firefox default profile name -------------------------------------------------------------------------------- 0.31s
firefox : debug profile_name ---------------------------------------------------------------------------------------------- 0.07s
```


