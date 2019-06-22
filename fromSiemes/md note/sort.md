### java sort note

#### 冒泡

~~~java
int[] nums = {1,2,3,4,5,6,7,77,10};
for(int i=0;i<nums.length-1;i++) {
    for(int j=0;j<nums.length-1-i;j++) {
        if (nums[j]>nums[j+1]) {
            int tem = nums[j];
            nums[j]=nums[j+1];
            nums[j+1]=tem;
        }
    }
}
~~~

