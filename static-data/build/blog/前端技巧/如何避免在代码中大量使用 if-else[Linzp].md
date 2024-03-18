首先要明确一点，所谓程序，就是用逻辑判断语句和循环语句串起来实现某种逻辑。所以逻辑判断语句是程序的基本要素，不用对此过于恐惧。

但是大量的不当使用的if-else确实是会让自己代码看起来十分糟糕，可读性差，不能测试，不可维护。这个地方确实需要优化的，但是记住，逻辑的固有复杂性导致其实你不能减少那个最小的判断逻辑数量。

再单元测试里面有个很重要的概念叫【圈复杂度】，具体概念可能有点抽象，但是可以简化一下，其实和算法复杂度类似，算法复杂度是看循环代码的层数，有N层就是2的N次方，是一个指数级膨胀的东西，圈复杂度也是类似的，你if里面嵌套if圈复杂度也会指数性上升，而圈复杂度是衡量代码复杂度的。所以降低代码复杂性的最有效的手段就是尽可能不要if里面套if。例如

```javascript
if(m===1){    
  if(n===2){       
    dosomething    
  } 
}else {
  if(n===2){       
    dosomething2    
  }else{
    otherthing
  } 
}
```

这种代码改造为

```javascript
if(m===1&&n===2){    
  dosomething
  return; 
}
if(m!==1&&n===2){
  dosomething2
  return;
}

otherthing
```

通过以上操作你可以让你的逻辑语句变得十分清晰，而且便于单元测试，提升代码可读性。但是我说过本质上他没有降低逻辑数量，所以我们需要通过切分模块，把原本复杂的逻辑，切分成数个简单逻辑模块，然后通过这些简单逻辑模块的相互调用来完成复杂的逻辑。例如

```javascript
if(m===1&&n===2){    
  dosomething
  return; 
}
if(m!==1&&n===2){
  dosomething2
  return;
}

otherthing
```

可以改造成

```javascript
function dosomeing1(){}

function dosomeing2(){}

function otherting(){}

function main(){
  if(m===1&&n===2){    
    dosomething1()
    return; 
  }
  if(m!==1&&n===2){
    dosomething2()
    return;
  }
  otherthing()
}

main();
```

上面这段代码虽然看起来更复杂了，但是它把逻辑控制和具体实现分离，如果三个函数分支里面只需要实现自己内部的逻辑，在单元测试的时候，可以单独测function dosomeing1，function dosomeing2，function otherting，function main，在测试对应模块的时候其他模块的调用可以mock掉直接返回正确结果，而上面的代码就只能一起测试，导致几块东西相互影响。

接下来，你可以通过各个模块的组合方式，让整个一大块的功能能有秩序的组合在一起，通过良好的模块命名和文档，就可以让整个程序看起来可读性高，易于单元测试，可靠性强。从而远离那种面条式的，让人一看就恨不得原地爆炸的代码
