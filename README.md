样式
._page_container {
    font-family: Helvetica Neue, Helvetica, PingFang SC, Hiragino Sans GB, Microsoft YaHei, SimSun, sans-serif;
    font-size: 13px;
    height: 28px;
    line-height: 28px;
    text-align: center;
    margin: 100px auto;
    user-select: none;
}

._page_container ._prev,
._page_container ._next,
._page_container ._home,
._page_container ._last {
    min-width: 30px;
    font-size: 13px;
    margin: 0 5px;
    border-radius: 2px;
    cursor: pointer;
}

._page_container ._prev,
._page_container ._next {
    font-weight: 700;
}

._page_container ._pages,
._page_container ._prev,
._page_container ._next,
._page_container ._home,
._page_container ._last,
._page_container ._jumper,
._page_container ._count,
._page_container ._jumper_input,
._page_container ._sizes,
._page_container ._sizes_text {
    display: inline-block;
    color: #606266;
}

._page_container ._prev,
._page_container ._next,
._page_container ._home,
._page_container ._last {
    min-width: 30px;
    font-size: 13px;
    margin: 0 5px;
    border-radius: 2px;
    cursor: pointer;
}

._page_container ._pages li {
    display: inline-block;
    color: #303133;
    font-weight: 700;
    min-width: 25px;
    text-align: center;
    margin: 0 5px;
    padding: 0 5px;
    border-radius: 2px;
    cursor: pointer;
}

._page_container li {
    list-style: none;
    vertical-align: top;
}

._disabled {
    cursor: not-allowed!important;
}

._active_2 {
    color: #409eff!important;
    cursor: pointer;
}

._page_container ._prev,
._page_container ._next {
    font-weight: 700;
}

._page_container ._prev,
._page_container ._next,
._page_container ._home,
._page_container ._last {
    min-width: 30px;
    font-size: 13px;
    margin: 0 5px;
    border-radius: 2px;
    cursor: pointer;
}

._page_container ._count {
    margin: 0 5px;
}

._page_container ._jumper {
    color: #606266;
    margin: 0 10px;
}

._page_container ._count {
    margin: 0 5px;
}

._page_container ._jumper ._jumper_input {
    font-size: 14px;
    color: #606266;
    width: 50px;
    height: 26px;
    text-align: center;
    margin: 0 5px;
    padding: 3px;
    border: 1px solid #dcdfe6;
    border-radius: 4px;
    background: 0 0;
    outline: none;
    box-sizing: border-box;
}


html
<div id="pages_1" style="margin-top:100px">
                <div class="_page_container">
                    <img src="../public/image/left.png" class="left" style="width:13px;cursor: pointer;" alt="上一页">
                    <div class="_pages _pages_2">
                        <%pagination.forEach(item => {%>
                            <a class="_pages_li_2">
                                <%=item%>
                            </a>
                            <%})%>
                    </div>
                    <img src="../public/image/right.png" class="right" onclick="rightClick()" onmousemove="rightMousemove('<%=nav.list%>')" style="width:13px;cursor: pointer;" alt="下一页">

                    <div class="_count">共 100 条</div>
                    <div class="_jumper">
                        <div class="_count">共 20 页</div>
                        <span>前往</span><input class="_jumper_input" type="number" onkeyup="keyup_submit(event,value)" min="1" max="20">
                        <span>页</span>
                    </div>
                </div>
            </div>



js
        <script>
            window.onload = function() {
                let lista = document.querySelectorAll('._pages_li_2')
                let left = document.querySelector('.left')
                let right = document.querySelector('.right')

                lista[0].className = '_pages_li_2 _active_2 _disabled'
                for (let i = 0; i < lista.length; i++) {
                    lista[i].onmouseover = function() {
                        for (let j = 0; j < lista.length; j++) {
                            if (this.className !== '_pages_li_2 _active_2 _disabled') {
                                this.className = '_pages_li_2'
                            }
                        }
                        if (this.className !== '_pages_li_2 _active_2 _disabled') {
                            this.className = '_pages_li_2 _active_2'
                        }
                    }
                    lista[i].onmouseout = function() {
                        for (let j = 0; j < lista.length; j++) {
                            if (this.className !== '_pages_li_2 _active_2 _disabled') {
                                this.className = '_pages_li_2'
                            }
                        }
                        if (this.className !== '_pages_li_2 _active_2 _disabled') {
                            this.className = '_pages_li_2'
                        }
                    }
                    lista[i].onclick = function() {
                        if (this.className !== '_pages_li_2 _active_2 _disabled') {
                            location.href = `http://localhost:7001/marketingCase/${this.text}`
                        }
                        for (let j = 0; j < lista.length; j++) {
                            lista[j].className = '_pages_li_2'
                        }
                        this.className = '_pages_li_2 _active_2 _disabled'
                    }
                }

                left.onmouseover = function() {
                    if (lista[0].text === '1') {
                        this.className = '_disabled'
                    }
                }
                left.onclick = function() {
                    if (this.className !== '_disabled') {
                        let value = lista[0].text
                        location.href = `http://localhost:7001/marketingCase/${--value}`
                    }
                }

                function rightMousemove(list) {
                    list = list.split(',')
                    let index = lista[lista.length - 1].text
                    if (index++ === list.length) {
                        right.className = '_disabled'
                    }
                }

                function rightClick() {
                    if (right.className !== '_disabled') {
                        let value = lista[lista.length - 1].text
                        location.href = `http://localhost:7001/marketingCase/${++value}`
                    }
                }

                function keyup_submit(e, value) {
                    const evt = window.event || e
                    if (evt.keyCode == 13) {
                        location.href = `http://localhost:7001/marketingCase/${value}`
                    }
                }
            }
        </script>

