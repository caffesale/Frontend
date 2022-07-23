# 수학에 관련된 작은 TIP

## 최대공약수(GCD)와 최소공배수(LCM)

<br>

최대공약수와 최소공배수는 유클리드 호제법을 사용하여 쉽게 구할 수 있다. 최대공약수는 재귀, 반복문 어느 쪽으로도 구할 수 있다. 최소공배수는 최대공약수를 구했다면 간단한 나눗셈 연산으로 산출 가능하다

```javascript

// 반복문을 통해 최대공약수 구하기
function gcd(a,b){
  let R;
  while((a%b) > 0){
    R = a % b;
    a = b;
    b = R;
  }
  return b;
}

// 재귀법을 이용해 최대공약수 구하기
function gcd(a,b){
  if(b == 0){
    return a;
  }
  else{
    return gcd(b, (a % b));
  }
}

//최소공배수 구하기
function lcm(a,b){
  return (a * b)/gcd(a,b);
}
```

## 소수 판별하기

<br> 소수는 반복문과 조건문, 혹은 에라토스테네스의 체를 활용해 구할 수 있다.

```javascript
// 에라토스테네스의 체
function isPrime(num) {
    let prime = num != 1;
    for(var i=2; i<Math.sqrt(num); i++) { // sqrtnum+1
        if(num % i == 0) {
            prime = false;
            break;
        }
    }
    return prime;
}

```

## 약수

    Tip 제곱근이 정수라면 약수의 갯수는 홀수이다.
