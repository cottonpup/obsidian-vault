---
Date: 2023-08-29
Type: Development
Tags: Meetup
---

https://resume.io/

# README 작성하기
https://www.freecodecamp.org/korean/news/gisheobeu-peurojegteue-rideumi-paileul-jal-jagseonghaneun-bangbeob/

1. 프로젝트 소개
	- 여러분의 애플리케이션이 무엇을 하는지
		- resume를 편하게 사용이 가능
	- 왜 그 기술을 사용했는지,
3. 프로젝트 구조
4. 실행 화면 + URL
5. 트러블 슈팅
	- 여러분이 당면했던 문제나 나중에 추가하고 싶은 기능이 무엇인지
6. 회고

-----

# defaultSkillSuggestions

디폴트 스킬 추천

---
# EditorView
- What is interface and why should I pass it as a Props?
	- a group of related properties and methods that describe an object, but neither provides implementation nor initialisation for them.
	- App에서 지금 isFullPreview props를 건내주고 있다. 그래서 interface를 통해 프로퍼티와 메서드를 정의할 수 있다. 
	- 인터페이스는 프로퍼티와 메소드를 가질 수 있다는 점에서 클래스와 유사하나 직접 인스턴스를 생성할 수 없고 모든 메소드는 추상 메소드이다. 단, 추상 클래스의 추상 메소드와 달리 abstract 키워드를 사용하지 않는다.

https://poiemaweb.com/typescript-interface

```
    // TODO: Why do I need useRef? And why do I give the value as a null???
    // 디폴트 값이 null
    const ref = useRef<HTMLDivElement>(null);
```


```js
    useEffect(() => {
        const TITLE_HEIGHT_PX = ref.current!.getBoundingClientRect().height;

        function scrollThenFix() {
            // console.log(TITLE_HEIGHT_PX, window.screenTop);
            if (window.scrollY > TITLE_HEIGHT_PX && !shouldFixHeader) {
                // console.log('FIX HEADER!!');
                setShouldFixHeader(true);
            } else if (window.scrollY <= TITLE_HEIGHT_PX && shouldFixHeader) {
                // console.log('UNFIX HEADER!!');
                setShouldFixHeader(false);
            }
        }

        window.addEventListener('scroll', scrollThenFix);
        return () => {
            window.removeEventListener('scroll', scrollThenFix);
        };
    }, [shouldFixHeader]);
```

- What is `getBoundingClientRect`?
- What is the value of `shouldFixHeader`? 
