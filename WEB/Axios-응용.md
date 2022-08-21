# 취소 요청 응용 

```javascript
// useEffect와 취소 토큰을 응용하면 유저가 갑자기 다른 페이지로 이동한 경우 이미 보낸 요청을 간단히 취소할 수 있다
//......

useEffect(() => {
    let isMounted = true;
    
    // fetch API등을 사용하는 경우 자바스크립트의 AbortController를 사용한다.
    // const controller = new AbortController();
    
    const CancelToken = axios.CancelToken;
    const source = CancelToken.source();
        
    const getUsers = async () => {
        try{
            const response = await axios.get('url', {
                cancelToken: source.token
            })
            isMounted && setUsers(response.data);
        }
        catch(err){
            console.log(err)
        }
    // ... ...
    


    
    // AbortController를 사용할 경우
        const getUsers = async () => {
        try{
            const response = await axios.get('url', {
                signal: controller.signal
            })
            isMounted && setUsers(response.data);
        }
        catch(err){
            console.log(err)
        }
    // ... ...

    
    
    return () => {
        isMounted = false;
        source.cancel(); 
        // AbortController를 사용할 경우
        // controller.abort();
        };
},[])



```
