<Carousel autoplay v-model="value2" loop :autoplaySpeed="80000" >

另外 样式里要加上这个  要不然就完蛋了哦
 &_list {
    display: flex;
    flex-direction: row;
  }
其他可以参考CarouselVerticalDemo
