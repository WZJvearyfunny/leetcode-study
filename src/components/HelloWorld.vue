
<template>
  <div class="hello">
    <button @click="load()">touch me</button>
    <button @click="back()">roll back</button>
    <button @click="generatorFor()">generator</button>
    <div class="up-triangle" />
    <p class="dotted-line">
      庭院深深，不知有多深？杨柳依依，飞扬起片片烟雾，一重重帘幕不知有多少层
    </p>
    <p class="coupon"><span>200</span>优惠券</p>
    <div style="width: 100vw">
      <button @click="callmebaby(1, 2)">debounce</button>
      <button @click="maxArea()">maxArea</button>
      <button @click="intToRoman()">intToRoman</button>
      <button @click="trap()">trap</button>
      <button @click="trap_tow()">trap_tow</button>
      <button @click="longestCommonPrefix()">longestCommonPrefix</button>
    </div>
    <div style="width: 100vw">
      <button @click="threeSum()">threeSum</button>
      <button @click="threeSumClosest()">threeSumClosest</button>
      <button @click="letterCombinations()">letterCombinations</button>
      <button @click="fourSum()">fourSum</button>
      <button @click="isValid()">isValid</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  methods: {
    load() {
      window.location.href = "https://www.baidu.com";
      // window.location.replace('https://www.baidu.com')
    },
    back() {
      window.history.go(-1);
    },
    generatorFor() {
      function* gener() {
        let n = 0;
        yield n;
        n++;
        return;
      }
      for (let x of gener()) {
        console.log(x);
      }
    },
    callmebaby(volume, data) {
      this.debounce(this.con(volume, data), 400);
    },
    con(volume, data) {
      console.log("change", volume, data);
    },
    debounce(func, delay = 500) {
      let context = this; // this指向发生变化，需要提出来
      let args = arguments;
      return (function () {
        if (context.timeout) {
          clearTimeout(context.timeout);
        }
        context.timeout = setTimeout(() => {
          func.apply(context, args);
        }, delay);
      })(); // 注意:我加了()
    },
    maxArea() {
      let height = [1, 8, 6, 2, 5, 4, 8, 3, 7];
      let maxNub = 0;
      let minLen = 0,
        maxLen = height.length - 1;
      while (minLen < maxLen) {
        let nub = Math.min(height[minLen], height[maxLen]);
        let len = maxLen - minLen;
        maxNub = Math.max(maxNub, nub * len);
        if (height[minLen] > height[maxLen]) {
          maxLen--;
        } else {
          minLen++;
        }
      }
      return maxNub;
    },
    intToRoman() {
      let num = 3;
      let i = 0,
        j = 0,
        k = 0,
        l = 0,
        q = ~~(num / 1000),
        b = ~~((num % 1000) / 100),
        s = ~~(((num % 1000) % 100) / 10),
        g = ~~(((num % 1000) % 100) % 10),
        romanNub = "";
      console.log(q);
      console.log(b);
      console.log(s);
      console.log(g);
      while (i < q) {
        romanNub += "M";
        i++;
      }
      if (b >= 5) {
        switch (b) {
          case 9:
            romanNub += "CM";
            break;
          default:
            romanNub += "D";
            while (j < b - 5) {
              romanNub += "C";
              j++;
            }
            break;
        }
      } else {
        switch (b) {
          case 4:
            romanNub += "CD";
            break;
          default:
            while (j < b) {
              romanNub += "C";
              j++;
            }
            break;
        }
      }
      if (s >= 5) {
        switch (s) {
          case 9:
            romanNub += "XC";
            break;
          default:
            romanNub += "L";
            while (k < s - 5) {
              romanNub += "X";
              k++;
            }
            break;
        }
      } else {
        switch (s) {
          case 4:
            romanNub += "XL";
            break;
          default:
            while (k < s) {
              romanNub += "X";
              k++;
            }
            break;
        }
      }
      if (g >= 5) {
        switch (g) {
          case 9:
            romanNub += "IX";
            break;
          default:
            romanNub += "V";
            while (l < g - 5) {
              romanNub += "I";
              l++;
            }
            break;
        }
      } else {
        switch (g) {
          case 4:
            romanNub += "IV";
            break;
          default:
            while (l < g) {
              romanNub += "I";
              l++;
            }
            break;
        }
      }
      console.log(romanNub);
      return romanNub;
    },
    trap() {
      let height = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1];
      const n = height.length;
      if (n == 0) {
        return 0;
      }

      const leftMax = new Array(n).fill(0);
      leftMax[0] = height[0];
      for (let i = 1; i < n; i++) {
        leftMax[i] = Math.max(leftMax[i - 1], height[i]);
      }
      const rightMax = new Array(n).fill(0);
      rightMax[0] = height[n - 1];
      for (let i = n - 2; i >= 0; i--) {
        rightMax[i] = Math.max(rightMax[i + 1], height[i]);
      }
      let ans = 0;
      for (let i = 0; i < n; i++) {
        ans += Math.min(leftMax[i], rightMax[i]) - height[i];
      }
      return ans;
    },
    trap_tow() {
      let height = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1];
      let left = 0,
        right = height.length - 1,
        leftMax = 0,
        rightMax = 0,
        ans = 0;
      while (left < right) {
        leftMax = Math.max(leftMax, height[left]);
        rightMax = Math.max(rightMax, height[right]);
        if (height[right] > height[left]) {
          ans += leftMax - height[left];
          left++;
        } else {
          ans += rightMax - height[right];
          right--;
        }
      }
      return ans;
    },
    longestCommonPrefix() {
      const strs = ["dog", "racecar", "car"];
      const strss = [];
      const preFixs = [];
      let maxLen = 0;
      strs.forEach((val) => {
        strss.push(val.split(""));
        maxLen = val.length > maxLen ? val.length : maxLen;
      });
      strss.forEach((val) => {
        if (maxLen > val.length) {
          for (let i = 0; i < maxLen - val.length + 1; i++) {
            val.push("-");
          }
        }
      });
      for (let i = 0; i < maxLen; i++) {
        const preFix = [];
        for (let j = 0; j < strss.length; j++) {
          if (i === 0) {
            if (!preFix.find((n) => n === strss[j][i])) {
              preFix.push(strss[j][i]);
            }
          } else {
            if (preFixs[i - 1].find((n) => n === strss[j][i - 1])) {
              if (!preFix.find((n) => n === strss[j][i])) {
                preFix.push(strss[j][i]);
              }
            }
          }
        }
        if (preFix.length > 1) break;
        preFixs.push(preFix);
      }
      let resultStr = "";
      preFixs.forEach((val) => {
        resultStr += val;
      });
      console.log(resultStr);
      return resultStr;
    },
    threeSum() {
      const nums = [-1, 0, 1, 2, -1, -4];
      if (nums.length < 3) {
        return [];
      }
      nums.sort((a, b) => {
        return a - b;
      });
      const resultNums = [];
      // for (let i = 0; i < nums.length; i++) {
      //   for (let j = i + 1; j < nums.length; j++) {
      //     for (let o = j + 1; o < nums.length; o++) {
      //       if (nums[i] + nums[j] + nums[o] === 0) {
      //         let issingle = true;
      //         if (resultNums.length === 0) {
      //           resultNums.push([nums[i], nums[j], nums[o]]);
      //         }
      //         if(resultNums.find(n=>{
      //           return n.toString()==[nums[i], nums[j], nums[o]].toString()
      //         })){
      //           issingle = false;
      //         }
      //         if (issingle) {
      //           resultNums.push([nums[i], nums[j], nums[o]]);
      //         }
      //       }
      //     }
      //   }
      // }
      let left = 0,
        mid = ~~(nums.length / 2),
        right = nums.length - 1;
      while (left < right) {
        const diff = 0 - nums[left] - nums[right];
        if (nums[mid] > diff) {
          while (left < mid) {
            mid--;
            let issingle = true;
            if (nums[mid] === diff) {
              if (resultNums.length === 0) {
                resultNums.push([nums[left], nums[mid], nums[right]]);
                mid = ~~(nums / 2);
                left++;
                break;
              }
              if (
                resultNums.find((n) => {
                  return (
                    n.toString() ==
                    [nums[left], nums[mid], nums[right]].toString()
                  );
                })
              ) {
                issingle = false;
              }
              if (issingle) {
                resultNums.push([nums[left], nums[mid], nums[right]]);
                mid = ~~(nums / 2);
                left++;
                break;
              }
            }
          }
        } else {
          while (mid < right) {
            mid++;
            let issingle = true;
            if (nums[mid] === diff) {
              if (resultNums.length === 0) {
                resultNums.push([nums[left], nums[mid], nums[right]]);
                mid = ~~(nums / 2);
                left++;
                break;
              }
              if (
                resultNums.find((n) => {
                  return (
                    n.toString() ==
                    [nums[left], nums[mid], nums[right]].toString()
                  );
                })
              ) {
                issingle = false;
              }
              if (issingle) {
                resultNums.push([nums[left], nums[mid], nums[right]]);
                mid = ~~(nums / 2);
                left++;
                break;
              }
            }
          }
        }
      }
      console.log(resultNums);
      return resultNums;
    },
    threeSumClosest() {
      let nums = [1, 1, 48, 50, 99, 100, 103, 333, 333],
        target = 250,
        ans = 999999999,
        sum = 0;
      nums.sort((a, b) => a - b);
      console.log(nums);
      for (let i = 0; i < nums.length; i++) {
        let left = i,
          mid = i + 1,
          right = nums.length - 1;
        if (nums[left] == 48) {
          console.log(true);
        }
        if (nums[left] > Math.abs(target) + 1) {
          break;
        }
        if (nums[left] == nums[left - 1]) continue;
        while (right > mid) {
          const cak = Math.abs(target - nums[left] - nums[mid] - nums[right]);
          if (ans > cak) {
            ans = cak;
            sum = nums[left] + nums[mid] + nums[right];
            while (
              right > mid &&
              nums[mid] == nums[mid + 1] &&
              nums[right] == nums[right - 1]
            ) {
              mid++;
              right--;
            }
            mid++;
            if (mid === right) {
              right--;
              mid = left + 1;
            }
            continue;
          }
          while (
            right > mid &&
            nums[mid] == nums[mid + 1] &&
            nums[right] == nums[right - 1]
          ) {
            mid++;
            right--;
          }
          mid++;
          if (mid >= right) {
            right--;
            mid = left + 1;
          }
        }
      }
      return sum;
    },
    letterCombinations() {
      const digits = "";
      let dictionaryList = {
        2: ["a", "b", "c"],
        3: ["d", "e", "f"],
        4: ["g", "h", "i"],
        5: ["j", "k", "l"],
        6: ["m", "n", "o"],
        7: ["p", "q", "r", "s"],
        8: ["t", "u", "v"],
        9: ["w", "x", "y", "z"],
      };
      let resultList = [];
      if (digits.length < 1) {
        return [];
      } else if (digits.length === 1) {
        return dictionaryList[digits[0]];
      }
      let forlist = (list) => {
        let delist = [];
        resultList.forEach((val) => {
          for (let i = 0; i < list.length; i++) {
            delist.push(val + list[i]);
          }
        });
        resultList = delist;
      };
      resultList = dictionaryList[digits[0]];
      for (let i = 1; i < digits.length; i++) {
        console.log(i);
        forlist(dictionaryList[digits[i]]);
      }
      return resultList;
    },
    fourSum() {
      let nums = [-1, 0, -5, -2, -2, -4, 0, 1, -2],
        target = -9,
        left = 0,
        mid1 = 1,
        mid2 = 2,
        right = nums.length - 1,
        resultList = [];
      nums.sort((a, b) => a - b);
      while (right > left) {
        if (nums[left] + nums[mid1] + nums[mid2] > target && target > 0) {
          return resultList;
        }
        while (mid2 > mid1 && right > mid2) {
          if (nums[left] + nums[mid1] + nums[mid2] + nums[right] === target) {
            resultList.push([nums[left], nums[mid1], nums[mid2], nums[right]]);
          }
          while (right > mid2 && nums[mid2] === nums[mid2 + 1]) {
            mid2++;
          }
          mid2++;
          if (mid2 >= right) {
            while (mid2 > mid1 && nums[mid1] === nums[mid1 + 1]) {
              mid1++;
            }
            mid1++;
            mid2 = mid1 + 1;
          }
        }
        while (right > left && nums[right] === nums[right - 1]) {
          right--;
        }
        right--;
        mid1 = left + 1;
        mid2 = left + 2;
        if (left >= right) {
          right = nums.length;
          while (right > left && nums[left] === nums[left + 1]) {
            left++;
          }
          left++;
          mid1 = left + 1;
          mid2 = left + 2;
        }
      }
      return resultList;
    },
    isValid() {
      const s = "{()}[]";
      if (s.length % 2 != 0) return false;
      const sList = []
      const kuohaozuo = ['{','(','[']
      for(let i = 0;i<s.length;i++){
        if(kuohaozuo.includes(s[i])){
          sList.push(s[i])
        }else{
          if(s[i]==='}'&&sList[sList.length-1]==='{'){
            sList.pop()
            continue
          }else if(s[i]===']'&&sList[sList.length-1]==='['){
            sList.pop()
            continue
          }else if(s[i]===')'&&sList[sList.length-1]==='('){
            sList.pop()
            continue
          }
          return false
        }
      }
      return !sList.length
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.up-triangle {
  width: 0;
  height: 0;
  border-style: solid;
  border-width: 0 0 25px 25px;
  border-color: transparent transparent rgb(0, 0, 0) transparent;
}
.dotted-line {
  width: 100%;
  margin: auto;
  padding: 20px;
  border: 1px dashed transparent;
  background: linear-gradient(white, white) padding-box,
    repeating-linear-gradient(60deg, red 0, #ccc 0.25em, white 0, white 0.75em);
}
.coupon {
  width: 300px;
  height: 100px;
  line-height: 100px; /* 行高 */
  margin: 50px auto;
  text-align: center;
  position: relative; /* 相对定位 */
  background: radial-gradient(circle at right bottom, transparent 10px, #fff 0)
      top right / 50% 50% no-repeat,
    radial-gradient(circle at left bottom, transparent 10px, #000 0) top left /
      50% 50% no-repeat,
    radial-gradient(circle at right top, transparent 10px, #000 0) bottom right /
      50% 50% no-repeat,
    radial-gradient(circle at left top, transparent 10px, #ffffff 0) bottom left /
      50% 50% no-repeat;
  filter: drop-shadow(2px 2px 2px rgba(0, 0, 0, 0.2));
}
.coupon span {
  display: inline-block;
  vertical-align: middle;
  margin-right: 10px;
  color: red;
  font-size: 50px;
  font-weight: 400;
}
</style>
