# 原创

： 已安装成功Django,import时依然提示ImportError: No module named Django。最后解决！！

# 已安装成功Django,import时依然提示ImportError: No module named Django。最后解决！！

学习笔记：python编程从入门到实践<br/> django 安装成功，但是输入命令python manage.py migrate时依旧出现“ImportError: No module named
Django”，按照许多大神教的寻找版本是否冲突已经无解。在idle上import也没有报错。这就说明确实存在django，版本正确。多次重复虚拟环境进入也没有问题，但是依然出现“ImportError: No module named
Django”。<br/> 找了一上午，才想到如果环境正确，模块存在，那出现的可能就是创建的虚拟环境不在模块范围内，属于虚拟环境中找不到模块的存在。于是重新创建虚拟环境，将之放在django模块的位置上才终于成功。
