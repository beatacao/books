### 第4章  

> 函数递归判断是否回文   
    
    function isPalindrome(str){
        if(str.length <= 1) return true;
        if(str.charAt(0) !== str.charAt(str.length-1)) return false;
        returrn isPalindrome(str.substring(1, str.length-2))
    }

>  利用闭包实现的函数重载  

    function addMethod(obj, name, fn){
        var old = obj[name]
        obj[name] = function(){
            if(fn.length === arguments.length){
                return fn.apply(this, arguments)
            }else{
                return old.apply(this, arguments)
            }
        }
    }

    var ninja = {
        values: ['a', 'b', 'c']
    }
    addMethod(ninja, 'find', function(){return this.values})
    addMethod(ninja, 'find', function(name){
        var ret = []
        for(var i=0; i < this.values.length; i++){
            if(this.values[i].indexOf(name) === 0){
                ret.push(this.values[i])
            }
        }
        return ret
    })  


    