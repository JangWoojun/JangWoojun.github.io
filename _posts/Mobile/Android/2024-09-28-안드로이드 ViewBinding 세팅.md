---
title: 안드로이드 ViewBinding 세팅
date: 2024-09-28 06:20:00 +/-0000
categories: [Mobile, Android]
tags: [android]
toc: true
pin: true
---

안드로이드 앱 개발을 하다 보면 초반에는 당연하게 썼던 findViewById가 곧 매우 불편하다는 것을 깨닫게 될 것이다 그래서 보통은 findViewById 대신 viewBinding이나 dataBinding을 사용하는데 이번에는 이 중 viewBinding을 사용하는 법에 대해 알아보겠다

# viewBinding 시작하기

viewBinding을 사용하는 법은 매우 간단한데 이번 글에서 차례 차례 소개하겠다
해당 글은 KTS 기준으로 설명하고 있다

## build.gradle

우선은 build.gradle에서 설정해줘야 되는 부분이 있다

~~~kotlin
plugins {
    ...
}

android {
    ...
    defaultConfig {
        ...
    }
    buildTypes {
        release {
            ...
        }
    }
    compileOptions {
        ...
    }
    viewBinding { // 이 부분 추가
        enable = true
    }
    kotlinOptions {
        ...
    }
}

dependencies {
    ...
}
~~~

앱 수준 build.gradle에 들어가면 위 코드처럼 생겼을 텐데 여기서 주석으로 표시해둔 것처럼

~~~kotlin
viewBinding {
    enable = true
}
~~~

해당 코드를 추가해주면 된다 이렇게 하면 viewBinding은 성공적으로 추가 되었다 그 후 viewBinding을 사용하려면 액티비티, 프래그먼트에서 세팅을 해줘야 한다

## Activity 설정

우선 액티비티 설정부터 알아보면

`Activity`

```xml
class MainActivity : AppCompatActivity() {
    private lateinit var binding: ActivityMainBinding
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)
    }
}
```

이렇게 해주면 되는데 여기서 binding 타입은 해당 액티비티 이름에 따라 달라진다 위 코드에선 ActivityMainBinding로 되어있는데 만약 액티비티가 SplashActivity라면 ActivitySplashBinding가 될 것이다 그 후 

onCreate에서 binding을 초기화해주고 setContentView에 binding.root를 넣어주면 된다

## Fragment 설정

프래그먼트는 상대적으로 액티비티보다 복잡해보지만 막상 자세히 보면 별게 없다

`Fragment`

```kotlin
class MainFragment : Fragment() {

    private var _binding: FragmentMainBinding? = null
    private val binding get() = _binding!!

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
    }

    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View {
        _binding = FragmentMainBinding.inflate(inflater, container, false)
        return binding.root
    }

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
    }

    override fun onDestroy() {
        super.onDestroy()
        _binding = null
    }

}
```

~~~kotlin
private var _binding: FragmentMainBinding? = null
private val binding get() = _binding!!
~~~

해당 부분 타입은 액티비티와 동일하게 이름에 맞게 해주면 되고 다음으로 onCreateView에서 _binding을 초기화 해준 뒤 binding.root를 return 해주면 된다

여기서 명심해야 할 점은 꼭 

~~~kotlin
override fun onDestroyView() {
    super.onDestroyView()
    _binding = null
}
~~~

onDestroyView에서 _binding을 null로 다시 초기화 시켜줘야 한다 그렇지 않으면 메모리 누수가 발생할 수 있다
