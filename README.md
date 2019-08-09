package com.example.a0109.test2;

import android.content.Intent;
import android.net.Uri;
import android.os.AsyncTask;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.text.method.ScrollingMovementMethod;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.IOException;
import java.sql.Date;
import java.text.SimpleDateFormat;


public class MainActivity extends AppCompatActivity {

    private String htmlPageUrl = "https://news.naver.com/main/ranking/popularDay.nhn?mid=etc&sid1=111";
    private TextView textviewHtmlDocument1;
    private TextView textviewHtmlDocument2;
    private TextView textviewHtmlDocument3;
    private TextView textviewHtmlDocument4;
    private TextView textviewHtmlDocument5;
    private TextView textviewHtmlDocument6;

    private String htmlContentInStringFormat1="";
    private String htmlContentInStringFormat2="";
    private String htmlContentInStringFormat3="";
    private String htmlContentInStringFormat4="";
    private String htmlContentInStringFormat5="";
    private String htmlContentInStringFormat6="";

    long now = System.currentTimeMillis();

    Date date = new Date(now);
    SimpleDateFormat sdf = new SimpleDateFormat("yyyyMMdd");

    String getTime = sdf.format(date);

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);


        textviewHtmlDocument1 = (TextView)findViewById(R.id.textView1);
        textviewHtmlDocument2 = (TextView)findViewById(R.id.textView2);
        textviewHtmlDocument3 = (TextView)findViewById(R.id.textView3);
        textviewHtmlDocument4 = (TextView)findViewById(R.id.textView4);
        textviewHtmlDocument5 = (TextView)findViewById(R.id.textView5);
        textviewHtmlDocument6 = (TextView)findViewById(R.id.textView6);

        textviewHtmlDocument1.setMovementMethod(new ScrollingMovementMethod());
        textviewHtmlDocument2.setMovementMethod(new ScrollingMovementMethod());
        textviewHtmlDocument3.setMovementMethod(new ScrollingMovementMethod());
        textviewHtmlDocument4.setMovementMethod(new ScrollingMovementMethod());
        textviewHtmlDocument5.setMovementMethod(new ScrollingMovementMethod());
        textviewHtmlDocument6.setMovementMethod(new ScrollingMovementMethod());


        Button htmlTitleButton = (Button)findViewById(R.id.button);
        htmlTitleButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                JsoupAsyncTask jsoupAsyncTask = new JsoupAsyncTask();
                jsoupAsyncTask.execute();
            }
        });
    }

    private class JsoupAsyncTask extends AsyncTask<Void, Void, Void> {

        @Override
        protected void onPreExecute() {
            super.onPreExecute();
        }

        @Override
        protected Void doInBackground(Void... params) {
            int i = 0;
            try {
                Document doc = Jsoup.connect(htmlPageUrl).get();
                Elements links = doc.select("div.ranking_section ol li dl dt a");

                for (Element link : links) {
//                    htmlContentInStringFormat += (link.attr("abs:href")
//                            + "("+link.text().trim() + ")\n");
                    if (i<5){
                        htmlContentInStringFormat1 += (link.text().trim() + "\n\n");
                    }else if(i<10){
                        htmlContentInStringFormat2 += (link.text().trim() + "\n\n");
                    }else if(i<15){
                        htmlContentInStringFormat3 += (link.text().trim() + "\n\n");
                    }else if(i<20){
                        htmlContentInStringFormat4 += (link.text().trim() + "\n\n");
                    }else if(i<25){
                        htmlContentInStringFormat5 += (link.text().trim() + "\n\n");
                    }else if(i<30){
                        htmlContentInStringFormat6 += (link.text().trim() + "\n\n");
                    }
                    i++;
                }

            } catch (IOException e) {
                e.printStackTrace();
            }
            return null;
        }

        @Override
        protected void onPostExecute(Void result) {
            textviewHtmlDocument1.setText(htmlContentInStringFormat1);
            textviewHtmlDocument2.setText(htmlContentInStringFormat2);
            textviewHtmlDocument3.setText(htmlContentInStringFormat3);
            textviewHtmlDocument4.setText(htmlContentInStringFormat4);
            textviewHtmlDocument5.setText(htmlContentInStringFormat5);
            textviewHtmlDocument6.setText(htmlContentInStringFormat6);

        }
    }

    public void poli(View v){
        Intent intent = new Intent(Intent.ACTION_VIEW);
        intent.setData(Uri.parse("https://news.naver.com/main/ranking/popularDay.nhn?rankingType=popular_day&sectionId=100&date=" + getTime));
        startActivity(intent);
    }
    public void eco(View v){
        Intent intent = new Intent(Intent.ACTION_VIEW);
        intent.setData(Uri.parse("https://news.naver.com/main/ranking/popularDay.nhn?rankingType=popular_day&sectionId=101&date=" + getTime));
        startActivity(intent);
    }
    public void soci(View v){
        Intent intent = new Intent(Intent.ACTION_VIEW);
        intent.setData(Uri.parse("https://news.naver.com/main/ranking/popularDay.nhn?rankingType=popular_day&sectionId=102&date=" + getTime));
        startActivity(intent);
    }public void cult(View v){
        Intent intent = new Intent(Intent.ACTION_VIEW);
        intent.setData(Uri.parse("https://news.naver.com/main/ranking/popularDay.nhn?rankingType=popular_day&sectionId=103&date=" + getTime));
        startActivity(intent);
    }
    public void world(View v){
        Intent intent = new Intent(Intent.ACTION_VIEW);
        intent.setData(Uri.parse("https://news.naver.com/main/ranking/popularDay.nhn?rankingType=popular_day&sectionId=104&date=" + getTime));
        startActivity(intent);
    }
    public void it(View v){
        Intent intent = new Intent(Intent.ACTION_VIEW);
        intent.setData(Uri.parse("https://news.naver.com/main/ranking/popularDay.nhn?rankingType=popular_day&sectionId=105&date=" + getTime));
        startActivity(intent);
    }
}

