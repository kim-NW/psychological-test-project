# psychological-test-project

## 방문자 수 firebase 상호작용으로 구현

Firebase 앱을 초기화하고, 연결

```
const app = initializeApp(firebaseConfig);
      const analytics = getAnalytics(app);
      const db = getFirestore(app);
```

Firebase Cloud Firestore counts의 counts 문서 참조
![image](https://user-images.githubusercontent.com/117978017/235393861-b1a5fb42-6efe-47d0-b301-6faf29e03465.png)

```
      const docRef = doc(db, "counts", "counts");
      const docSnap = await getDoc(docRef);
```

count문서가 존재한다면, 버튼 클릭 수를 카운트에 저장

```
      if (docSnap.exists()) {
        const button = document.querySelector('.start_btn');
        let cnt = docSnap.data().count
        function clickCount() {
          cnt += 1;
          setDoc(doc(db, "counts", "counts"), {
            count: cnt,
          });
        }
        button.addEventListener('click', clickCount);
```

Firestore 업데이트된 값을 저장하고 HTML 요소에 저장된 클릭 수 표시

```
        const countt = document.querySelector('.countt');
        countt.innerHTML = "총 이용자 수는 : " + cnt;
      }
```

counts문서가 존재하지 않으면 콘솔에 작성한 메세지가 뜨게 설정

```
      else {
        // doc.data() will be undefined in this case
        console.log("No such document!");
      }
```



