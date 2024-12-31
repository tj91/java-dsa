


Approach
- treat tiring and non tiring days as +1 and -1 
    - finding subarray with sum = 1
    - sum = 1 makes sure that num tiring > num non tiring
      






```java

    public int longestWPI(int[] hours) {

        int l = hours.length;
        Map<Integer, Integer> map = new HashMap<>();
        int prefSum = 0, resLen = 0;
        for(int i = 0;i < l ;i++){

            prefSum += (hours[i] > 8) ? 1 : -1;

            if(prefSum > 0){
                resLen = i + 1;
            } else if(map.containsKey(prefSum - 1)){
                resLen = Math.max(resLen, i - map.get(prefSum-1));
            }

            if(!map.containsKey(prefSum)){
                map.put(prefSum,i);
            }

        }

        return resLen;
    }



```
