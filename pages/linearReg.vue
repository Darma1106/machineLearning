<template>
  <div>linearReg-手写线性回归</div>
</template>

<script lang="ts" setup>
// 线性回归
// 实现一个线性回归模型
// (wx+b - y)^2

const datas: [number, number][] = []
for (let i = 0; i < 100; i++) {
  datas.push([i, i])
}

const lossFn = (datas: [number, number][], w: number, b: number) => {
  let kw = 0
  let kb = 0
  datas.forEach(([xCurrent, yCurrent]) => {
    kw += (2 / datas.length) * (w * xCurrent + b - yCurrent) * xCurrent
    kb += (2 / datas.length) * (w * xCurrent + b - yCurrent)
  })

  return [kw, kb]
}

const linearReg = (datas: [number, number][], originW: number, originB: number, rate: number, time = 1000) => {
  let w = originW,
    b = originB
  for (let index = 0; index < time; index++) {
    const [kw, kb] = lossFn(datas, w, b)

    w = w - kw * rate
    b = b - kb * rate
  }
  return [w, b]
}

onMounted(() => {
  console.log(linearReg(datas, 0, 0, 0.0001))
})
</script>
