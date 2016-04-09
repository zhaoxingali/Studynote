# swig 渲染引擎

标签（空格分隔）： 学习笔记

--
###swig js模板引擎
  <pre>1. 根据路径渲染页面;
2. 面向对象的模板继承，页面复用
3. 面向对象的模板继承
4. 动态页面
5. 功能强大</pre>

###swig的使用

    1.swig变量
    //变量未定义输出为空
    {{foo.bar}}
    {{foo['bar']}}
    
    2.swig标签
        a.模板继承: extends 
            //layout.html
            <!doctype html>
            <html>
            <head>
                <meta charset="utf-8">
                <title>{% block title %}My Site{% endblock %}</title>
                {% block head %}
                {% endblock %}
            </head>
            <body>
                {% block content %}{% endblock %}
            </body>
            </html>
            {% extends './layout.html' %}
            {% block title %}My Page{% endblock %}
            {% block head %}
            {% parent %}
            {% endblock %}
            {% block content %}
            <p>This is just an awesome page.</p>
            <h1>hello,lego.</h1>
            <script>
                //require('pages/index/main');
            </script>
            {% endblock %}
            
        b.定义块使之可以重写模板或者重写父模板的同名块：block
        
        c.将父模板中同名块注入当前块：parent
        
        d.引用一个模板：include
        
        e.停止解析标记中的内容：raw
        
        f.遍历数组和对象:for
        {% for x in object %}
            <p>{{ x }}</p>
        {% endfor %}
        
        g.条件语句：if
        {% if foo %}
                <p>{{ foo }}</p>
        {% else %}
                <p>error</p>
        {% endif %}
        
        h.修改当前变量的自定义转换类型：autoescape
        {% autoescape false%}//未做数据类型转换
            {{ output }}
        {% endautoescape%}
        {% autoescape true 'js' %}//做数据类型转换
            {{ output }}
        {% endautoescape%}
        
        i.设置一个变量，在当前上下文中复用
        {% set foo = [0,1,2,3,4] %}