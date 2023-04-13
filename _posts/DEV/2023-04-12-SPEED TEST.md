---
title: 생애 첫 프로젝트 회고록 - 반응 속도 테스트 
date: 2023-04-12 21:30:55 +/-0000
categories: [DEV, MEMOIR]
tags: [dev, memoir]
toc: true
pin: true
---

# 생애 첫 프로젝트를 마치고...

## 프로젝트 소개 
<img width="1440" alt="스크린샷 2022-11-05 오후 10 26 05" src="https://user-images.githubusercontent.com/102157871/200122241-9a1bae2d-12e4-4a55-a036-e48723ce05aa.png">

[반응 속도 테스트](https://play.google.com/store/apps/details?id=com.speedtest.clickgame)는 웹사이트들에서 플레이할 수 있었던 반응속도 테스트를 안드로이드 앱으로 구현한 프로젝트로 
그 전까지 클론 코딩으로 여러 앱이나 웹을 따라 만들기만 한 내가 진행한 생애 첫 프로젝트이다.

- 플랫폼 : 안드로이드/모바일
- 사용 언어 : Kotlin
- 진행 기간: 2022. 10. 12 ~ 2022. 10. 21 (20일)
- 진행 인원: 개인 프로젝트 (1인)
- [깃허브 리포지토리](https://github.com/JangWoojun/Click_Game)
- [플레이 스토어](https://play.google.com/store/apps/details?id=com.speedtest.clickgame)

## 개발 배경

사실 해당 프로젝트를 하기 전 난 강의를 보며 클론 코딩만 하고 간단한 앱을 만들더라도 클론 코딩으로 만든 앱을 조금씩 바꾸는 식으로 밖에 안했기에

내 스스로 만든 것이 아닌 강의를 보고 만들었는데 이건 초등학생도 할 수 있는 타자연습 그 이상 그 이하도 아니라는 생각이 들고 이건 내 것이 아닌 강사의 프로젝트다라는 생각이 들어 스스로 프로젝트를 진행봐야겠다고 결심하게 되었다.

<img width="1440" alt="스크린샷 2023-04-12 오전 9 59 44" src="https://user-images.githubusercontent.com/102157871/231320244-b6e934f8-cb97-4816-bb5c-cab39b33944c.png">

그러던 중 **2022년에 다양한 유튜버들과 프로게이머**들이 **반응속도 테스트**를 하는 모습들을 유튜브에 올리며 **학생들** 사이에서 **핫해진** 반응속도 테스트를

**웹 사이트**가 아닌 **모바일 애플리케이션**으로 하면 어떨까? 사람들이 많이 쓰지 않을까? 라는 가벼운 발상이 떠올라 이를 주제로 만들어보게 되었다.

## 사용 예제

### 1인 플레이
![main](https://user-images.githubusercontent.com/102157871/200124245-fe108f01-01ca-4324-a7b7-a69ecf648465.gif)

![main3](https://user-images.githubusercontent.com/102157871/200124248-8ca2860c-b81e-4b61-9ac3-3e82d08667b5.gif)

### 2인 플레이

![2](https://user-images.githubusercontent.com/102157871/200124293-220de4ca-019b-4450-ad17-19cccc9048ca.gif)

플레이 모습 위와 같으며 1인과 2인으로 나눠서 만들었다.

## 구현 기능

- 반응속도 테스트
    - 랜덤한 시간동안 대기하다가 클릭으로 바뀌었을 때 버튼을 클릭하여 반응속도를 측정
    - 반응속도를 다섯 번을 측정하여 그 평균 값을 보여주는 기능
    - 반응속도 측정으로 바뀌기 전에 미리 클릭할 경우 부정행위로 감지해 초기화하는 기능
- 2인 플레이 기능
    - 다른 친구와 함께 2인으로 반응속도를 측정하여 승자를 가리는 기능

## 이슈

### 랜덤한 간격으로 코드 실행이 안되는 이슈

~~~kotlin
class MainActivity : AppCompatActivity() {
    var time = 0
    var totalTime = 0
    var started = false

    val TAG = "GameActivity"

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        val gameLayout = findViewById<ConstraintLayout>(R.id.mainView)
        val clickBtn = findViewById<Button>(R.id.clickBtn)
        val count = findViewById<TextView>(R.id.count)
        val timeCheck = findViewById<TextView>(R.id.timeCheck)


        for (i in 1..5){
            val num = (500..5000).random()
            Log.d(TAG,num.toString())
            Handler(Looper.getMainLooper()).postDelayed({

                start()
                gameLayout.setBackgroundColor(Color.parseColor("#90ee90"))
                timeCheck.setTextColor(Color.parseColor("#90ee90"))
                clickBtn.text = "Click"

                clickBtn.setOnClickListener {
                    stop()
                    count.text = "$i/5"
                    timeCheck.text = "${time}ms"
                    timeCheck.setTextColor(Color.parseColor("#ffffff"))
                    totalTime+=time
                    time=0
                }
            }, num.toLong())
        }
    }

    fun start(){
        started = true
        thread(start=true) {
            while (true){
                if (!started) break

                Thread.sleep(1)
                time+=1
            }
        }
    }

    fun stop(){
        started=false
        val gameLayout = findViewById<ConstraintLayout>(R.id.mainView)
        val clickBtn = findViewById<Button>(R.id.clickBtn)
        gameLayout.setBackgroundColor(Color.parseColor("#FFEA7D"))
        clickBtn.text = "Ready"
    }
}
~~~

위 코드는 처음 구상한 코드로 내가 원하는 로직은

랜덤한 시간 이후 반응 속도를 클릭하는 화면으로 바뀌고 여기서 버튼을 누른다면 다시 시작화면으로 바꾸고 이것을 for문을 통해 5번 반복하는 것을 원했었다 하지만...

{% include embed/youtube.html id='xFs88kWmUi8' %}

해당 코드에 이슈를 정리하면 아래와 같다

1. 반응속도 테스트 횟수가 3~5회 랜덤하게 바뀐다
1. 테스트 횟수가 1, 2, 3 이렇게 순차적인 것이 아닌 1, 4, 3, 5 이런 식으로 규칙이 없다

해당 원인을 시간이 지나 지금보면 어느 부분이 문제인지 바로 알겠으나 당시에는 코딩을 배운 지와 안드로이드 앱 개발 자체를 얼마 안됐기도 하고 첫 프로젝트라 원인을 감을 못 잡았었다

~~~kotlin
for (i in 1..5) {
    val num = (500..5000).random()
    Log.d(TAG,num.toString())
    Handler(Looper.getMainLooper()).postDelayed({

        start()
        gameLayout.setBackgroundColor(Color.parseColor("#90ee90"))
        timeCheck.setTextColor(Color.parseColor("#90ee90"))
        clickBtn.text = "Click"

        clickBtn.setOnClickListener {
            stop()
            count.text = "$i/5"
            timeCheck.text = "${time}ms"
            timeCheck.setTextColor(Color.parseColor("#ffffff"))
            totalTime+=time
            time=0
        }
    }, num.toLong())
}
~~~

당시에는 코드 지연(실행중)에서 내가 버튼을 눌러야만 코드 실행이 끝난 것으로 간주하고 그제서야 다시 for 문으로 다시 처음부터 실행하는 것을 생각했고 그래서 로직을 저렇게 구성한 것 같다

지금와서 생각해본다면 Handler에서 지연 실행되는 코드를 for문으로 반복시키는 것이 빠르게 실행되니 중첩되어서 동시에 실행이 되어 화면이 바뀌는 것이 이미 바뀌어 있어 안먹히고 테스트 횟수 또한 랜덤한 값이 더 크게 나온 것이 적용되어 그런 것 같다

그래서 해당 문제를 당시에는

~~~kotlin
class GameActivity : AppCompatActivity() {
    private var time = 0
    private var totalTime = 0
    private var started = false
    private var chk = false
    private var num = 0
    private var backPressedTime : Long = 0
    private lateinit var binding:ActivityGameBinding

    private var i = 1

    private val handler = Handler(Looper.getMainLooper())


    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_game)
        binding = ActivityGameBinding.inflate(layoutInflater)
        setContentView(binding.root)

        num = (2000..4000).random()

        handler.postDelayed({

            start()

        }, num.toLong())

        binding.clickBtn.setOnClickListener {
            if (chk){
                if(i==5){
                    val intent = Intent(this,MaxScoreActivity::class.java)
                    totalTime/=5
                    intent.putExtra("maxScore",totalTime.toString())
                    intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TASK)
                    intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK)
                    startActivity(intent)
                    overridePendingTransition(R.anim.vertical_enter, R.anim.none)
                }
                stop(i)
                i++
                chk =false
                num = (3000..5000).random()
                handler.postDelayed({

                    start()

                }, num.toLong())
            }
            else {
                binding.resetBtn.visibility = View.VISIBLE
                binding.soon1.visibility = View.VISIBLE
                binding.soon2.visibility = View.VISIBLE
                binding.timeCheck.visibility = View.INVISIBLE
                binding.waitText.visibility = View.INVISIBLE
                binding.clickText.visibility = View.INVISIBLE
                binding.clickBtn.visibility = View.INVISIBLE

                handler.removeCallbacksAndMessages(null)
                time = 0
                totalTime = 0
                i = 0
                binding.gameLayout.setBackgroundColor(Color.parseColor("#a9cbd7"))
                binding.count.text = getString(R.string.count,i)

                binding.resetBtn.setOnClickListener {
                    reset()
                    i++
                }
            }
        }

    }

    private fun start(){

        binding.soon1.visibility = View.INVISIBLE
        binding.soon2.visibility = View.INVISIBLE
        binding.resetBtn.visibility = View.INVISIBLE
        binding.gameLayout.setBackgroundColor(Color.parseColor("#2dd12d"))
        binding.timeCheck.visibility = View.INVISIBLE
        binding.waitText.visibility = View.INVISIBLE
        binding.clickText.visibility = View.VISIBLE
        binding.clickBtn.text = getString(R.string.Click)
        binding.clickBtn.visibility = View.VISIBLE

        chk = true
        started = true
        thread(start=true) {

            while (true){
                if (!started) break

                Thread.sleep(1)
                time+=1
            }

        }
    }

    private fun stop(i:Int){

        started=false

        binding.gameLayout.setBackgroundColor(Color.parseColor("#c0102a"))
        binding.clickBtn.text = getString(R.string.Ready)
        binding.count.text = getString(R.string.count,i)
        binding.timeCheck.text = getString(R.string.timeCheck,time)
        binding.timeCheck.visibility = View.VISIBLE
        binding.waitText.visibility = View.VISIBLE
        binding.clickText.visibility = View.INVISIBLE
        binding.waitText.text = getString(R.string.game_guidance)

        totalTime+=time
        time=0
    }

    private fun reset(){

        binding.resetBtn.visibility = View.INVISIBLE
        binding.soon1.visibility = View.INVISIBLE
        binding.soon2.visibility = View.INVISIBLE
        binding.clickBtn.visibility = View.VISIBLE
        binding.waitText.visibility = View.VISIBLE

        binding.gameLayout.setBackgroundColor(Color.parseColor("#c0102a"))
        time = 0
        totalTime = 0
        i = 0

        val num = (3000..5000).random()

        handler.postDelayed({

            start()

        }, num.toLong())

    }

}
~~~

이런 식으로 들어오자마자 지연 실행을 실행하다가 만약 버튼을 클릭한다면 준비화면으로 바꾼 후 다시 지연 실행을 시키면서 그러다 반복 횟수가 5가 되면 종료하는 식으로 구성했다

### 랭킹 시스템 구현 문제

처음에 구상했을 때는 2인 플레이로 만드는 것이 아니라 랭킹 시스템을 구현하여 반응 속도가 빠른 순위를 기록하는 걸 목표로 했었다 하지만 당시에 내가 생각했을 때 랭킹을 구현하는 것은 난이도가 너무 높을 거 같고 어떻게 구현할 지 감이 안잡혀서 

랭킹 구현 말고 좀 더 쉬운 다른 구현이 없을까? 고민을 하다가 두명이서 하나의 폰으로 구현할 수 있게 하는 것으로 계획을 바꿨다

## 느낀점

앞에서 설명한 것과 같이 반응 속도 테스트는 클론 코딩 강의나 책을 보고 따라 만들거나 조금 수정한 프로젝트가 아닌 내가 스스로 생각하고 처음부터 끝까지 만들어 본 프로젝트였기에 내게 뜻깊은 프로젝트이다 

해당 프로젝트를 통해 나는 내가 클론 코딩으로 남이 만든 것이 아닌 스스로도 하나의 프로젝트를 완성할 수 있다는 자신감과 나도 이제 어디가서 작고 초라하지만 남들에게 보여줄 수 있는 개인 프로젝트가 생겼다는 점에서 감격스러웠다

하지만 여기서 느끼고 반성한 점이 있다면 주석처리를 잘 해두자는 것과 프로젝트를 진행하면서 겪은 이슈나 버그들은 꼭 어딘가에 기록해두자는 것이다 해당 작업들을 하지 않았더니 남이 볼 때나 시간이 지나 볼 때 코드를 한눈에 이것이 어떤 기능인 지 알아보기 힘들고

나중에 회고록을 적을 때도 어떤 이슈가 있었고 어떻게 버그를 해결했는지 기억하여 적기가 힘들었다 또한 해당 프로젝트는 시험기간에 진행하여 공부와 프로젝트 둘다 잡으려다보니 시간적으로 매우 촉박하고 힘들었기에 다음부터는 둘중 하나를 선택하여 집중하던지 다른일이 없을 시기에 해야겠다

