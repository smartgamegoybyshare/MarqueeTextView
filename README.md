# MarqueeView

可垂直跑、可水平跑的跑馬燈

### 效果圖

<img src="/resources/MarqueeView.gif" style="width: 30%;">

#### Gradle Project:

	allprojects {
		repositories {
			...
			maven { url 'https://jitpack.io' }
		}
	}
	
#### Gradle Module:

    implementation 'com.github.smartgamegoybyshare:MarqueeTextView:1.0.1'
	
#### 屬性

| Attribute 屬性          | Description 描述 | 
|:---				     |:---| 
| mvAnimDuration         | 一行文字動畫執行時間 | 
| mvInterval         | 兩行文字翻頁時間間隔 | 
| mvTextSize         | 文字大小 | 
| mvTextColor         | 文字顏色 | 
| mvGravity         | 文字位置:left、center、right | 
| mvSingleLine         | 單行設置 |
| mvDirection        | 動畫滾動方向:bottom_to_top、top_to_bottom、right_to_left、left_to_right |
| mvFont             | 設置字體 |

#### XML

    <com.smart.marqueeview.MarqueeView
        android:id="@+id/marqueeView"
        android:layout_width="match_parent"
        android:layout_height="30dp"
        app:mvAnimDuration="1000"
        app:mvDirection="bottom_to_top"
        app:mvInterval="3000"
        app:mvTextColor="@color/white"
        app:mvTextSize="14sp"
        app:mvSingleLine="true"
        app:mvFont="@font/yourFont"/>

#### 設置TextView列表數據，或者設置自定義的Model數據類型

    MarqueeView marqueeView = (MarqueeView) findViewById(R.id.marqueeView);

    List<String> messages = new ArrayList<>();
    messages.add("1. This is testtext。");
    messages.add("2. Welcome！");
    messages.add("3. Java HelloWorld");
    marqueeView.startWithList(messages);

    // 或者設置自定義的Model數據類型
    public class CustomModel implements IMarqueeItem {
        @Override
        public CharSequence marqueeMessage() {
            return "...";
        }
    }

    List<CustomModel> messages = new ArrayList<>();
    marqueeView.startWithList(messages);
    
    // 設置自己的動畫
    marqueeView.startWithList(messages, R.anim.anim_bottom_in, R.anim.anim_top_out);

#### 設置字串數據

    String message = "若要天幫，不如求人，若要求人，不如求己，凡事都必經學習之痛苦";
    marqueeView.startWithText(message);
    
    // 設置自己的動畫
    marqueeView.startWithText(message, R.anim.anim_bottom_in, R.anim.anim_top_out);

#### 設置事件監聽

    marqueeView.setOnItemClickListener(new MarqueeView.OnItemClickListener() {
        @Override
        public void onItemClick(int position, TextView textView) {
            Toast.makeText(getApplicationContext(), String.valueOf(marqueeView1.getPosition()) + ". " + textView.getText(), Toast.LENGTH_SHORT).show();
        }
    });

#### 重影問題可参考以下解決方案

在 Activity 或 Fragment 中

    @Override
    public void onStart() {
        super.onStart();
        marqueeView.startFlipping();
    }

    @Override
    public void onStop() {
        super.onStop();
        marqueeView.stopFlipping();
    }

在 ListView 或 RecyclerView 的 Adapter 中

    @Override
    public void onViewDetachedFromWindow(@NonNull ViewHolder holder) {
        super.onViewDetachedFromWindow(holder);
        holder.marqueeView.stopFlipping();
    }

<br/>

### 關於

此庫由sunfusheng所提供之MarqueeView庫改變而成
請支持原文
[GitHub: sunfusheng](https://github.com/sunfusheng/MarqueeView) 