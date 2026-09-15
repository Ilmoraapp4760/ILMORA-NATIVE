name: Build ILMORA Native APK

on:
  push:
    paths: ['.github/workflows/build-apk.yml']
  workflow_dispatch:

permissions:
  contents: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '17'

      - uses: gradle/actions/setup-gradle@v3
        with:
          gradle-version: '8.7'

      - name: Write project files
        run: |
          mkdir -p app/src/main/java/com/ilmora/app app/src/main/res/layout app/src/main/res/drawable app/src/main/res/values
          cat > settings.gradle <<'EOF'
          pluginManagement {
              repositories { google(); mavenCentral(); gradlePluginPortal() }
          }
          dependencyResolutionManagement {
              repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
              repositories { google(); mavenCentral() }
          }
          rootProject.name = 'ILMORA'
          include ':app'
          EOF
          cat > gradle.properties <<'EOF'
          org.gradle.jvmargs=-Xmx2048m -Dfile.encoding=UTF-8
          android.useAndroidX=true
          EOF
          cat > app/build.gradle <<'EOF'
          plugins {
              id 'com.android.application' version '8.5.2'
          }
          android {
              namespace 'com.ilmora.app'
              compileSdk 34
              defaultConfig {
                  applicationId 'com.ilmora.app'
                  minSdk 24
                  targetSdk 34
                  versionCode 1
                  versionName '1.0'
              }
              compileOptions {
                  sourceCompatibility JavaVersion.VERSION_17
                  targetCompatibility JavaVersion.VERSION_17
              }
          }
          EOF
          cat > app/src/main/AndroidManifest.xml <<'EOF'
          <?xml version="1.0" encoding="utf-8"?>
          <manifest xmlns:android="http://schemas.android.com/apk/res/android">
              <uses-permission android:name="android.permission.INTERNET"/>
              <uses-permission android:name="android.permission.POST_NOTIFICATIONS"/>
              <uses-permission android:name="android.permission.FOREGROUND_SERVICE"/>
              <uses-permission android:name="android.permission.FOREGROUND_SERVICE_MEDIA_PLAYBACK"/>
              <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>
              <uses-permission android:name="android.permission.WAKE_LOCK"/>
              <uses-permission android:name="android.permission.VIBRATE"/>
              <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
              <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
              <application
                  android:label="ILMORA"
                  android:icon="@drawable/ic_app"
                  android:theme="@android:style/Theme.Material.NoActionBar">
                  <activity android:name=".MainActivity" android:exported="true"
                      android:configChanges="orientation|screenSize|keyboardHidden">
                      <intent-filter>
                          <action android:name="android.intent.action.MAIN"/>
                          <category android:name="android.intent.category.LAUNCHER"/>
                      </intent-filter>
                  </activity>
                  <activity android:name=".QiblaActivity" android:exported="false"/>
                  <activity android:name=".QuranActivity" android:exported="false"/>
                  <activity android:name=".AzkarActivity" android:exported="false"/>
                  <activity android:name=".TasbeehActivity" android:exported="false"/>
                  <service android:name=".AdhanService" android:exported="false"

android:foregroundServiceType="mediaPlayback"/>
                  <receiver android:name=".BootReceiver" android:exported="true">
                      <intent-filter>
                          <action android:name="android.intent.action.BOOT_COMPLETED"/>
                      </intent-filter>
                  </receiver>
              </application>
          </manifest>
          EOF
          cat > app/src/main/res/drawable/ic_app.xml <<'EOF'
          <?xml version="1.0" encoding="utf-8"?>
          <vector xmlns:android="http://schemas.android.com/apk/res/android"
              android:width="108dp" android:height="108dp"
              android:viewportWidth="108" android:viewportHeight="108">
              <path android:fillColor="#0C4A3C" android:pathData="M0,0h108v108h-108z"/>
              <path android:fillColor="#E7D3A4" android:pathData="M54,20c-13,11 -22,20 -22,30h44c0,-10 -9,-19 -22,-30z"/>
              <path android:fillColor="#C9A24F" android:pathData="M28,54h52v34h-52z"/>
              <path android:fillColor="#0C4A3C" android:pathData="M49,64h10v24h-10z"/>
              <path android:fillColor="#0C4A3C" android:pathData="M36,60h8v28h-8z"/>
              <path android:fillColor="#0C4A3C" android:pathData="M64,60h8v28h-8z"/>
          </vector>
          EOF
          cat > app/src/main/res/values/colors.xml <<'EOF'
          <?xml version="1.0" encoding="utf-8"?>
          <resources>
              <color name="green_deep">#0C4A3C</color>
              <color name="green_ink">#123F35</color>
              <color name="gold">#C9A24F</color>
              <color name="gold_soft">#E7D3A4</color>
              <color name="cream">#F6F1E7</color>
              <color name="ink">#1E2B27</color>
          </resources>
          EOF
          cat > app/src/main/res/layout/activity_main.xml <<'EOF'
          <?xml version="1.0" encoding="utf-8"?>
          <ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="match_parent" android:layout_height="match_parent"
              android:background="@color/cream">
              <LinearLayout android:layout_width="match_parent" android:layout_height="wrap_content"
                  android:orientation="vertical" android:padding="18dp">
                  <TextView android:id="@+id/header" android:layout_width="wrap_content" android:layout_height="wrap_content"
                      android:text="ILMORA" android:textColor="@color/green_deep" android:textSize="30sp" android:textStyle="bold"/>
                  <TextView android:layout_width="wrap_content" android:layout_height="wrap_content"
                      android:text="Pure • Simple • Spiritual" android:textColor="@color/gold" android:textSize="13sp"/>
                  <TextView android:id="@+id/nextPrayer" android:layout_width="match_parent" android:layout_height="wrap_content"
                      android:layout_marginTop="18dp" android:background="@color/green_deep" android:padding="18dp"
                      android:textColor="@color/gold_soft" android:textSize="18sp" android:textStyle="bold"/>
                  <TextView android:id="@+id/dateLine" android:layout_width="wrap_content" android:layout_height="wrap_content"
                      android:layout_marginTop="8dp" android:textColor="@color/ink" android:textSize="13sp"/>
                  <LinearLayout android:id="@+id/timesBox" android:layout_width="match_parent" android:layout_height="wrap_content"
                      android:orientation="vertical" android:layout_marginTop="10dp"/>
                  <TextView android:layout_width="wrap_content" android:layout_height="wrap_content"
                      android:layout_marginTop="18dp" android:text="Explore" android:textColor="@color/green_deep"

android:textSize="17sp" android:textStyle="bold"/>
                  <LinearLayout android:layout_width="match_parent" android:layout_height="wrap_content"
                      android:orientation="horizontal" android:layout_marginTop="8dp">
                      <Button android:id="@+id/btnQibla" android:layout_width="0dp" android:layout_height="70dp"
                          android:layout_weight="1" android:layout_marginEnd="6dp" android:text="Qibla" android:textSize="15sp"/>
                      <Button android:id="@+id/btnQuran" android:layout_width="0dp" android:layout_height="70dp"
                          android:layout_weight="1" android:layout_marginStart="6dp" android:text="Quran" android:textSize="15sp"/>
                  </LinearLayout>
                  <LinearLayout android:layout_width="match_parent" android:layout_height="wrap_content"
                      android:orientation="horizontal" android:layout_marginTop="8dp">
                      <Button android:id="@+id/btnAzkar" android:layout_width="0dp" android:layout_height="70dp"
                          android:layout_weight="1" android:layout_marginEnd="6dp" android:text="Azkar" android:textSize="15sp"/>
                      <Button android:id="@+id/btnTasbeeh" android:layout_width="0dp" android:layout_height="70dp"
                          android:layout_weight="1" android:layout_marginStart="6dp" android:text="Tasbeeh" android:textSize="15sp"/>
                  </LinearLayout>
                  <Button android:id="@+id/btnAdhan" android:layout_width="match_parent" android:layout_height="wrap_content"
                      android:layout_marginTop="16dp" android:text="Adhan Alerts: ON"/>
                  <TextView android:layout_width="match_parent" android:layout_height="wrap_content"
                      android:layout_marginTop="10dp" android:textSize="11sp" android:textColor="@color/ink"
                      android:text="Adhan plays at every prayer time — even when the app is closed or the phone restarts. Set ILMORA to Unrestricted battery for best results."/>
              </LinearLayout>
          </ScrollView>
          EOF
          cat > app/src/main/res/layout/activity_qibla.xml <<'EOF'
          <?xml version="1.0" encoding="utf-8"?>
          <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="match_parent" android:layout_height="match_parent"
              android:orientation="vertical" android:background="@color/cream" android:gravity="center_horizontal">
              <TextView android:layout_width="wrap_content" android:layout_height="wrap_content"
                  android:layout_marginTop="30dp" android:text="Qibla Direction" android:textColor="@color/green_deep"
                  android:textSize="24sp" android:textStyle="bold"/>
              <com.ilmora.app.CompassView android:id="@+id/compass"
                  android:layout_width="300dp" android:layout_height="300dp" android:layout_marginTop="20dp"/>
              <TextView android:id="@+id/qiblaInfo" android:layout_width="match_parent" android:layout_height="wrap_content"
                  android:gravity="center" android:padding="16dp" android:textColor="@color/ink" android:textSize="14sp"
                  android:text="Requesting…"/>
          </LinearLayout>
          EOF
          cat > app/src/main/res/layout/activity_quran.xml <<'EOF'
          <?xml version="1.0" encoding="utf-8"?>
          <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="match_parent" android:layout_height="match_parent"
              android:orientation="vertical" android:background="@color/cream">
              <TextView android:id="@+id/quranTitle" android:layout_width="match_parent" android:layout_height="wrap_content"

android:padding="14dp" android:text="Quran — 114 Surah" android:textColor="@color/green_deep"
                  android:textSize="20sp" android:textStyle="bold"/>
              <ListView android:id="@+id/quranList" android:layout_width="match_parent" android:layout_height="match_parent"/>
          </LinearLayout>
          EOF
          cat > app/src/main/res/layout/activity_azkar.xml <<'EOF'
          <?xml version="1.0" encoding="utf-8"?>
          <ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="match_parent" android:layout_height="match_parent"
              android:background="@color/cream">
              <LinearLayout android:id="@+id/azkarBox" android:layout_width="match_parent" android:layout_height="wrap_content"
                  android:orientation="vertical" android:padding="16dp"/>
          </ScrollView>
          EOF
          cat > app/src/main/res/layout/activity_tasbeeh.xml <<'EOF'
          <?xml version="1.0" encoding="utf-8"?>
          <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="match_parent" android:layout_height="match_parent"
              android:orientation="vertical" android:background="@color/cream" android:gravity="center">
              <TextView android:layout_width="wrap_content" android:layout_height="wrap_content"
                  android:text="Tasbeeh Counter" android:textColor="@color/green_deep" android:textSize="24sp" android:textStyle="bold"/>
              <Spinner android:id="@+id/preset" android:layout_width="220dp" android:layout_height="wrap_content"
                  android:layout_marginTop="14dp" android:background="@color/gold_soft"/>
              <Button android:id="@+id/count" android:layout_width="200dp" android:layout_height="200dp"
                  android:layout_marginTop="26dp" android:textSize="34sp" android:text="0"/>
              <Button android:id="@+id/reset" android:layout_width="wrap_content" android:layout_height="wrap_content"
                  android:layout_marginTop="20dp" android:text="Reset"/>
          </LinearLayout>
          EOF
          cat > app/src/main/java/com/ilmora/app/Data.java <<'EOF'
          package com.ilmora.app;

          public class Data {
              public static final String[] AZKAR_AR = {
                  "أَعُوذُ بِاللَّهِ مِنَ الشَّيْطَانِ الرَّجِيمِ. اللَّهُ لَا إِلَهَ إِلَّا هُوَ الْحَيُّ الْقَيُّومُ لَا تَأْخُذُهُ سِنَةٌ وَلَا نَوْمٌ…",
                  "أَصْبَحْنَا وَأَصْبَحَ الْمُلْكُ لِلَّهِ، وَالْحَمْدُ لِلَّهِ، لَا إِلَهَ إِلَّا اللَّهُ وَحْدَهُ لَا شَرِيكَ لَهُ",
                  "اللَّهُمَّ أَنْتَ رَبِّي لَا إِلَهَ إِلَّا أَنْتَ، خَلَقْتَنِي وَأَنَا عَبْدُكَ",
                  "لَا حَوْلَ وَلَا قُوَّةَ إِلَّا بِاللَّهِ",
                  "سُبْحَانَ اللَّهِ وَبِحَمْدِهِ، سُبْحَانَ اللَّهِ الْعَظِيمِ",
                  "أَسْتَغْفِرُ اللَّهَ وَأَتُوبُ إِلَيْهِ",
                  "اللَّهُمَّ صَلِّ وَسَلِّمْ عَلَى نَبِيِّنَا مُحَمَّدٍ"
              };
              public static final String[] AZKAR_EN = {
                  "Ayat al-Kursi (2:255) — the greatest verse; recite morning & night",
                  "Morning dhikr — 'We have entered the morning and all sovereignty belongs to Allah' (Muslim)",
                  "Sayyid al-Istighfar — the master of seeking forgiveness (Bukhari & Muslim)",
                  "La hawla — 'a treasure from the treasures of Paradise' (Bukhari & Muslim)",
                  "SubhanAllahi wa bihamdih — 'light on the tongue, heavy on the Scale' (Bukhari & Muslim)",
                  "Seek forgiveness 100 times daily (Bukhari & Muslim)",
                  "Salawat — 'whoever sends one salawat, Allah sends ten mercies' (Muslim)"
              };

public static final String[] TASBEEH = {
                  "SubhanAllah ×33", "Alhamdulillah ×33", "Allahu Akbar ×34",
                  "La ilaha illallah ×100", "Astaghfirullah ×100", "Salawat ×100"
              };
              public static final int[] TASBEEH_TARGET = {33, 33, 34, 100, 100, 100};
          }
          EOF
          cat > app/src/main/java/com/ilmora/app/MainActivity.java <<'EOF'
          package com.ilmora.app;

          import android.Manifest;
          import android.app.Activity;
          import android.content.Intent;
          import android.content.SharedPreferences;
          import android.content.pm.PackageManager;
          import android.os.Build;
          import android.os.Bundle;
          import android.os.Handler;
          import android.view.View;
          import android.widget.Button;
          import android.widget.LinearLayout;
          import android.widget.TextView;
          import android.widget.Toast;

          import org.json.JSONObject;

          import java.io.BufferedReader;
          import java.io.InputStreamReader;
          import java.net.HttpURLConnection;
          import java.net.URL;
          import java.nio.charset.StandardCharsets;
          import java.text.SimpleDateFormat;
          import java.util.Calendar;
          import java.util.Date;
          import java.util.Iterator;
          import java.util.Locale;

          public class MainActivity extends Activity {
              private JSONObject timings;
              private final Handler h = new Handler();
              private SharedPreferences prefs;
              private boolean loaded = false;

              private final Runnable clock = new Runnable() { public void run() { tickClock(); h.postDelayed(this, 1000); } };

              @Override
              protected void onCreate(Bundle b) {
                  super.onCreate(b);
                  setContentView(R.layout.activity_main);
                  prefs = getSharedPreferences("ilmora_native", MODE_PRIVATE);
                  if (Build.VERSION.SDK_INT >= 33 &&
                      checkSelfPermission(Manifest.permission.POST_NOTIFICATIONS) != PackageManager.PERMISSION_GRANTED) {
                      requestPermissions(new String[]{Manifest.permission.POST_NOTIFICATIONS}, 1);
                  }
                  startAdhanService();
                  ((Button) findViewById(R.id.btnQibla)).setOnClickListener(new View.OnClickListener() {
                      public void onClick(View v) { startActivity(new Intent(MainActivity.this, QiblaActivity.class)); }
                  });
                  ((Button) findViewById(R.id.btnQuran)).setOnClickListener(new View.OnClickListener() {
                      public void onClick(View v) { startActivity(new Intent(MainActivity.this, QuranActivity.class)); }
                  });
                  ((Button) findViewById(R.id.btnAzkar)).setOnClickListener(new View.OnClickListener() {
                      public void onClick(View v) { startActivity(new Intent(MainActivity.this, AzkarActivity.class)); }
                  });
                  ((Button) findViewById(R.id.btnTasbeeh)).setOnClickListener(new View.OnClickListener() {
                      public void onClick(View v) { startActivity(new Intent(MainActivity.this, TasbeehActivity.class)); }
                  });
                  ((Button) findViewById(R.id.btnAdhan)).setOnClickListener(new View.OnClickListener() {
                      public void onClick(View v) {
                          boolean on = !prefs.getBoolean("adhanOn", true);
                          prefs.edit().putBoolean("adhanOn", on).apply();
                          updateAdhanBtn();
                          Toast.makeText(MainActivity.this, on ? "Adhan alerts ON" : "Adhan alerts OFF", Toast.LENGTH_SHORT).show();
                          if (on) startAdhanService();
                      }
                  });
                  updateAdhanBtn();
                  fetchTimings();
              }

private void updateAdhanBtn() {
                  ((Button) findViewById(R.id.btnAdhan)).setText(
                      prefs.getBoolean("adhanOn", true) ? "Adhan Alerts: ON" : "Adhan Alerts: OFF");
              }

              private void startAdhanService() {
                  Intent svc = new Intent(this, AdhanService.class);
                  if (Build.VERSION.SDK_INT >= 26) startForegroundService(svc); else startService(svc);
              }

              @Override
              protected void onResume() { super.onResume(); clock.run(); }

              @Override
              protected void onPause() { super.onPause(); h.removeCallbacks(clock); }

              private void fetchTimings() {
                  new Thread(new Runnable() {
                      public void run() {
                          try {
                              HttpURLConnection c = (HttpURLConnection) new URL("https://api.aladhan.com/v1/timings?method=1").openConnection();
                              c.setConnectTimeout(8000); c.setReadTimeout(8000);
                              BufferedReader r = new BufferedReader(new InputStreamReader(c.getInputStream(), StandardCharsets.UTF_8));
                              StringBuilder sb = new StringBuilder();
                              String line;
                              while ((line = r.readLine()) != null) sb.append(line);
                              r.close();
                              JSONObject j = new JSONObject(sb.toString());
                              timings = j.getJSONObject("data").getJSONObject("timings");
                              AdhanService.timingsJson = timings.toString();
                              runOnUiThread(new Runnable() { public void run() { loaded = true; renderTimes(); } });
                          } catch (final Exception e) {
                              runOnUiThread(new Runnable() {
                                  public void run() {
                                      ((TextView) findViewById(R.id.nextPrayer)).setText("Connect to internet once — prayer times will load");
                                  }
                              });
                          }
                      }
                  }).start();
              }

              private void renderTimes() {
                  LinearLayout box = (LinearLayout) findViewById(R.id.timesBox);
                  box.removeAllViews();
                  if (timings == null) return;
                  String[] names = {"Fajr", "Sunrise", "Dhuhr", "Asr", "Maghrib", "Isha"};
                  for (String n : names) {
                      String t = timings.optString(n, "");
                      if (t.length() < 5) continue;
                      TextView tv = new TextView(this);
                      tv.setText(n + "   —   " + t.substring(0, 5));
                      tv.setTextSize(16f);
                      tv.setTextColor(0xFF1E2B27);
                      tv.setPadding(6, 10, 6, 10);
                      box.addView(tv);
                  }
              }

              private void tickClock() {
                  ((TextView) findViewById(R.id.dateLine)).setText(
                      new SimpleDateFormat("EEEE, d MMMM yyyy", Locale.US).format(new Date()));
                  if (!loaded || timings == null) return;
                  renderTimes();
                  int nowM = Calendar.getInstance().get(Calendar.HOUR_OF_DAY) * 60 + Calendar.getInstance().get(Calendar.MINUTE);
                  String[] order = {"Fajr", "Dhuhr", "Asr", "Maghrib", "Isha"};
                  String nextN = null; int nextM = -1;
                  for (String n : order) {
                      String t = timings.optString(n, "");
                      if (t.length() < 5) continue;

int m = Integer.parseInt(t.substring(0, 2)) * 60 + Integer.parseInt(t.substring(3, 5));
                      if (m > nowM) { nextN = n; nextM = m; break; }
                  }
                  String txt;
                  if (nextN == null) {
                      String t = timings.optString("Fajr", "");
                      int m = -60;
                      if (t.length() >= 5) m = Integer.parseInt(t.substring(0, 2)) * 60 + Integer.parseInt(t.substring(3, 5));
                      nextN = "Fajr (tomorrow)"; nextM = m + 1440;
                  }
                  int left = nextM - nowM;
                  txt = "Next: " + nextN + "  •  in " + (left / 60) + "h " + (left % 60) + "m";
                  ((TextView) findViewById(R.id.nextPrayer)).setText(txt);
              }
          }
          EOF
          cat > app/src/main/java/com/ilmora/app/CompassView.java <<'EOF'
          package com.ilmora.app;

          import android.content.Context;
          import android.graphics.Canvas;
          import android.graphics.Paint;
          import android.view.View;

          public class CompassView extends View {
              public volatile float heading = 0f;
              public volatile float qibla = 151.62f;
              private final Paint ring = new Paint(Paint.ANTI_ALIAS_FLAG);
              private final Paint gold = new Paint(Paint.ANTI_ALIAS_FLAG);
              private final Paint green = new Paint(Paint.ANTI_ALIAS_FLAG);
              private final Paint red = new Paint(Paint.ANTI_ALIAS_FLAG);
              private final Paint text = new Paint(Paint.ANTI_ALIAS_FLAG);

              public CompassView(Context c) {
                  super(c);
                  ring.setColor(0xFFC9A24F); ring.setStyle(Paint.Style.STROKE); ring.setStrokeWidth(6f);
                  gold.setColor(0xFFC9A24F);
                  green.setColor(0xFF0C4A3C);
                  red.setColor(0xFFB91C1C);
                  text.setColor(0xFF1E2B27); text.setTextSize(34f); text.setTextAlign(Paint.Align.CENTER);
              }

              public void setHeading(float deg) { heading = deg; invalidate(); }
              public void setQibla(float deg) { qibla = deg; invalidate(); }

              @Override
              protected void onDraw(Canvas cv) {
                  super.onDraw(cv);
                  float cx = getWidth() / 2f, cy = getHeight() / 2f, r = Math.min(cx, cy) - 12f;
                  cv.drawCircle(cx, cy, r, ring);
                  cv.drawCircle(cx, cy, 14f, green);
                  cv.save();
                  cv.rotate(qibla - heading, cx, cy);
                  Paint np = new Paint(gold);
                  cv.drawCircle(cx, cy - r * 0.55f, 22f, np);
                  cv.drawRect(cx - 5f, cy - r * 0.55f, cx + 5f, cy - 30f, np);
                  cv.restore();
                  cv.drawText("N", cx, cy - r + 40f, text);
                  cv.drawText("KAABA", cx, cy + r - 26f, np);
              }
          }
          EOF
          cat > app/src/main/java/com/ilmora/app/QiblaActivity.java <<'EOF'
          package com.ilmora.app;

          import android.Manifest;
          import android.app.Activity;
          import android.content.pm.PackageManager;
          import android.hardware.Sensor;
          import android.hardware.SensorEvent;
          import android.hardware.SensorEventListener;
          import android.hardware.SensorManager;
          import android.location.Location;
          import android.location.LocationListener;
          import android.location.LocationManager;
          import android.os.Build;
          import android.os.Bundle;
          import android.widget.TextView;

          public class QiblaActivity extends Activity implements SensorEventListener {
              private SensorManager sm;
              private CompassView cv;
              private TextView info;
              private float[] rot = new float[9];
              private float[] ori = new float[3];
              private double lat = Double.NaN, lon = Double.NaN;

@Override
              protected void onCreate(Bundle b) {
                  super.onCreate(b);
                  setContentView(R.layout.activity_qibla);
                  cv = (CompassView) findViewById(R.id.compass);
                  info = (TextView) findViewById(R.id.qiblaInfo);
                  sm = (SensorManager) getSystemService(SENSOR_SERVICE);
                  if (Build.VERSION.SDK_INT >= 23 &&
                      checkSelfPermission(Manifest.permission.ACCESS_COARSE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
                      requestPermissions(new String[]{Manifest.permission.ACCESS_COARSE_LOCATION, Manifest.permission.ACCESS_FINE_LOCATION}, 2);
                  } else {
                      grabLocation();
                  }
              }

              private void grabLocation() {
                  try {
                      LocationManager lm = (LocationManager) getSystemService(LOCATION_SERVICE);
                      Location l = null;
                      if (lm != null) {
                          l = lm.getLastKnownLocation(LocationManager.GPS_PROVIDER);
                          Location n = lm.getLastKnownLocation(LocationManager.NETWORK_PROVIDER);
                          if (l == null || (n != null && n.getTime() > l.getTime())) l = n;
                      }
                      if (l != null) { onLocation(l); return; }
                      if (lm != null) {
                          lm.requestLocationUpdates(LocationManager.NETWORK_PROVIDER, 0, 0, new LocationListener() {
                              public void onLocationChanged(Location l) { onLocation(l); }
                              public void onProviderDisabled(String p) {}
                              public void onProviderEnabled(String p) {}
                              public void onStatusChanged(String p, int s, Bundle e) {}
                          });
                      }
                      info.setText("Turn ON location and step outside once — Qibla will lock on");
                  } catch (Exception e) {
                      info.setText("Location unavailable — showing default Qibla bearing");
                  }
              }

              private void onLocation(Location l) {
                  lat = l.getLatitude(); lon = l.getLongitude();
                  double kl = Math.toRadians(21.4225), klo = Math.toRadians(39.8262);
                  double la = Math.toRadians(lat), lo = Math.toRadians(lon);
                  double dlo = klo - lo;
                  double y = Math.sin(dlo), x = Math.cos(la) * Math.tan(kl) - Math.sin(la) * Math.cos(dlo);
                  double brg = (Math.toDegrees(Math.atan2(y, x)) + 360) % 360;
                  cv.setQibla((float) brg);
                  double dlon = klo - lon;
                  double dist = 6371 * Math.acos(Math.min(1, Math.sin(Math.toRadians(lat)) * Math.sin(kl)
                      + Math.cos(Math.toRadians(lat)) * Math.cos(kl) * Math.cos(dlon)));
                  info.setText(String.format(java.util.Locale.US, "Qibla: %.1f° from North • Kaaba: %.0f km", brg, dist));
              }

              @Override
              protected void onResume() {
                  super.onResume();
                  Sensor s = sm.getDefaultSensor(Sensor.TYPE_ROTATION_VECTOR);
                  if (s == null) s = sm.getDefaultSensor(Sensor.TYPE_ORIENTATION);
                  if (s != null) sm.registerListener(this, s, SensorManager.SENSOR_DELAY_GAME);
              }

              @Override
              protected void onPause() { super.onPause(); sm.unregisterListener(this); }

              @Override
              public void onSensorChanged(SensorEvent e) {
                  if (e.sensor.getType() == Sensor.TYPE_ROTATION_VECTOR) {
                      SensorManager.getRotationMatrixFromVector(rot, e.values);

SensorManager.getOrientation(rot, ori);
                      float az = (float) ((Math.toDegrees(ori[0]) + 360) % 360);
                      cv.setHeading(az);
                  } else if (e.sensor.getType() == Sensor.TYPE_ORIENTATION) {
                      cv.setHeading((float) ((e.values[0] + 360) % 360));
                  }
              }

              @Override
              public void onAccuracyChanged(Sensor s, int a) {}

              @Override
              public void onRequestPermissionsResult(int code, String[] p, int[] g) {
                  if (code == 2) grabLocation();
              }
          }
          EOF
          cat > app/src/main/java/com/ilmora/app/QuranActivity.java <<'EOF'
          package com.ilmora.app;

          import android.app.Activity;
          import android.app.AlertDialog;
          import android.os.Bundle;
          import android.widget.ArrayAdapter;
          import android.widget.ListView;
          import android.widget.TextView;
          import android.widget.Toast;

          import org.json.JSONArray;
          import org.json.JSONObject;

          import java.io.BufferedReader;
          import java.io.InputStreamReader;
          import java.net.HttpURLConnection;
          import java.net.URL;
          import java.nio.charset.StandardCharsets;

          public class QuranActivity extends Activity {
              private ListView list;
              private TextView title;
              private JSONArray surahs = null;

              @Override
              protected void onCreate(Bundle b) {
                  super.onCreate(b);
                  setContentView(R.layout.activity_quran);
                  list = (ListView) findViewById(R.id.quranList);
                  title = (TextView) findViewById(R.id.quranTitle);
                  loadSurahs();
                  list.setOnItemClickListener((parent, v, pos, id) -> {
                      if (surahs == null) return;
                      try {
                          JSONObject s = surahs.getJSONObject(pos);
                          openSurah(s.getInt("number"), s.getString("name"), s.getInt("numberOfAyahs"));
                      } catch (Exception e) { Toast.makeText(this, "Error", Toast.LENGTH_SHORT).show(); }
                  });
              }

              private void loadSurahs() {
                  new Thread(() -> {
                      try {
                          String j = get("https://api.alquran.cloud/v1/surah");
                          surahs = new JSONObject(j).getJSONArray("data");
                          String[] rows = new String[surahs.length()];
                          for (int i = 0; i < surahs.length(); i++) {
                              JSONObject s = surahs.getJSONObject(i);
                              rows[i] = s.getInt("number") + ". " + s.getString("name") + " — " + s.getString("englishName") + " (" + s.getInt("numberOfAyahs") + ")";
                          }
                          final String[] f = rows;
                          runOnUiThread(() -> list.setAdapter(new ArrayAdapter<>(this, android.R.layout.simple_list_item_1, f)));
                      } catch (Exception e) {
                          runOnUiThread(() -> Toast.makeText(this, "Internet se connect karo — Quran list load nahi hui", Toast.LENGTH_LONG).show());
                      }
                  }).start();
              }

              private void openSurah(int num, String name, int ayahs) {
                  title.setText("Surah " + name);
                  new Thread(() -> {
                      try {
                          String j = get("https://api.alquran.cloud/v1/surah/" + num + "/editions/quran-uthmani,en.sahih");
                          JSONArray eds = new JSONObject(j).getJSONArray("data");

JSONArray ar = eds.getJSONObject(0).getJSONArray("ayahs");
                          JSONArray en = eds.getJSONObject(1).getJSONArray("ayahs");
                          String[] rows = new String[ar.length()];
                          for (int i = 0; i < ar.length(); i++) {
                              rows[i] = ar.getJSONObject(i).getString("text") + "\n" + (i + 1) + ". " + en.getJSONObject(i).getString("text");
                          }
                          final String[] f = rows;
                          runOnUiThread(() -> {
                              list.setAdapter(new ArrayAdapter<>(QuranActivity.this, android.R.layout.simple_list_item_1, f));
                              AlertDialog.Builder ab = new AlertDialog.Builder(QuranActivity.this);
                          });
                      } catch (Exception e) {
                          runOnUiThread(() -> Toast.makeText(this, "Load nahi hua — internet check karo", Toast.LENGTH_SHORT).show());
                      }
                  }).start();
              }

              private String get(String url) throws Exception {
                  HttpURLConnection c = (HttpURLConnection) new URL(url).openConnection();
                  c.setConnectTimeout(10000); c.setReadTimeout(15000);
                  BufferedReader r = new BufferedReader(new InputStreamReader(c.getInputStream(), StandardCharsets.UTF_8));
                  StringBuilder sb = new StringBuilder();
                  String line;
                  while ((line = r.readLine()) != null) sb.append(line);
                  r.close();
                  return sb.toString();
              }
          }
          EOF
          cat > app/src/main/java/com/ilmora/app/AzkarActivity.java <<'EOF'
          package com.ilmora.app;

          import android.app.Activity;
          import android.graphics.Color;
          import android.os.Bundle;
          import android.view.Gravity;
          import android.widget.LinearLayout;
          import android.widget.ScrollView;
          import android.widget.TextView;

          public class AzkarActivity extends Activity {
              @Override
              protected void onCreate(Bundle b) {
                  super.onCreate(b);
                  setContentView(R.layout.activity_azkar);
                  LinearLayout box = (LinearLayout) findViewById(R.id.azkarBox);
                  TextView head = new TextView(this);
                  head.setText("Azkar & Authentic Adhkar");
                  head.setTextSize(22f); head.setTextColor(Color.parseColor("#0C4A3C"));
                  box.addView(head);
                  for (int i = 0; i < Data.AZKAR_AR.length; i++) {
                      TextView card = new TextView(this);
                      card.setText(Data.AZKAR_AR[i] + "\n\n" + Data.AZKAR_EN[i]);
                      card.setTextSize(15f); card.setTextColor(Color.parseColor("#1E2B27"));
                      card.setBackgroundColor(Color.WHITE);
                      card.setPadding(34, 34, 34, 34);
                      LinearLayout.LayoutParams lp = new LinearLayout.LayoutParams(
                          LinearLayout.LayoutParams.MATCH_PARENT, LinearLayout.LayoutParams.WRAP_CONTENT);
                      lp.topMargin = 26;
                      card.setLayoutParams(lp);
                      box.addView(card);
                  }
                  TextView foot = new TextView(this);
                  foot.setText("All adhkar above are from authentic sources (Bukhari, Muslim, Abu Dawud).");
                  foot.setTextSize(12f); foot.setTextColor(Color.parseColor("#5A6B66"));
                  foot.setGravity(Gravity.CENTER);
                  LinearLayout.LayoutParams fp = new LinearLayout.LayoutParams(
                      LinearLayout.LayoutParams.MATCH_PARENT, LinearLayout.LayoutParams.WRAP_CONTENT);

fp.topMargin = 40;
                  foot.setLayoutParams(fp);
                  box.addView(foot);
              }
          }
          EOF
          cat > app/src/main/java/com/ilmora/app/TasbeehActivity.java <<'EOF'
          package com.ilmora.app;

          import android.app.Activity;
          import android.content.Context;
          import android.os.Build;
          import android.os.Bundle;
          import android.os.VibrationEffect;
          import android.os.Vibrator;
          import android.view.View;
          import android.widget.AdapterView;
          import android.widget.ArrayAdapter;
          import android.widget.Button;
          import android.widget.Spinner;
          import android.widget.Toast;

          public class TasbeehActivity extends Activity {
              private int count = 0, target = 33;

              @Override
              protected void onCreate(Bundle b) {
                  super.onCreate(b);
                  setContentView(R.layout.activity_tasbeeh);
                  Spinner sp = (Spinner) findViewById(R.id.preset);
                  Button btn = (Button) findViewById(R.id.count);
                  Button reset = (Button) findViewById(R.id.reset);
                  sp.setAdapter(new ArrayAdapter<>(this, android.R.layout.simple_list_item_1, Data.TASBEEH));
                  sp.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
                      public void onItemSelected(AdapterView<?> p, View v, int pos, long id) {
                          target = Data.TASBEEH_TARGET[pos]; count = 0; btn.setText(String.valueOf(count));
                      }
                      public void onNothingSelected(AdapterView<?> p) {}
                  });
                  btn.setOnClickListener(new View.OnClickListener() {
                      public void onClick(View v) {
                          count++;
                          btn.setText(String.valueOf(count));
                          if (count >= target) {
                              buzz();
                              Toast.makeText(TasbeehActivity.this, "MashaAllah — " + target + " complete!", Toast.LENGTH_SHORT).show();
                              count = 0;
                              btn.postDelayed(() -> btn.setText("0"), 350);
                          }
                      }
                  });
                  reset.setOnClickListener(new View.OnClickListener() {
                      public void onClick(View v) { count = 0; btn.setText("0"); }
                  });
              }

              private void buzz() {
                  try {
                      Vibrator vm = (Vibrator) getSystemService(Context.VIBRATOR_SERVICE);
                      if (vm == null) return;
                      if (Build.VERSION.SDK_INT >= 26) vm.vibrate(VibrationEffect.createOneShot(120, VibrationEffect.DEFAULT_AMPLITUDE));
                      else vm.vibrate(120);
                  } catch (Exception e) {}
              }
          }
          EOF
          cat > app/src/main/java/com/ilmora/app/AdhanService.java <<'EOF'
          package com.ilmora.app;

          import android.app.Notification;
          import android.app.NotificationChannel;
          import android.app.NotificationManager;
          import android.app.PendingIntent;
          import android.app.Service;
          import android.content.Intent;
          import android.content.SharedPreferences;
          import android.media.AudioManager;
          import android.media.MediaPlayer;
          import android.os.Build;
          import android.os.Handler;
          import android.os.IBinder;
          import android.os.PowerManager;

          import org.json.JSONObject;

          import java.io.BufferedReader;

import java.io.InputStreamReader;
          import java.net.HttpURLConnection;
          import java.net.URL;
          import java.nio.charset.StandardCharsets;
          import java.text.SimpleDateFormat;
          import java.util.Calendar;
          import java.util.Date;
          import java.util.Iterator;
          import java.util.Locale;

          public class AdhanService extends Service {
              public static volatile String timingsJson = null;
              private static final String ADHAN = "https://cdn.aladhan.com/audio/adhans/a9.mp3";
              private final Handler h = new Handler();
              private MediaPlayer mp;
              private JSONObject timings;
              private String fired = "";
              private SharedPreferences prefs;

              private final Runnable loop = new Runnable() { public void run() { tick(); h.postDelayed(this, 30000); } };

              @Override
              public void onCreate() {
                  super.onCreate();
                  prefs = getSharedPreferences("ilmora_native", MODE_PRIVATE);
                  goForeground("Adhan alerts are active");
                  h.postDelayed(loop, 4000);
              }

              @Override
              public int onStartCommand(Intent i, int f, int id) { return START_STICKY; }

              @Override
              public IBinder onBind(Intent i) { return null; }

              @Override
              public void onDestroy() { h.removeCallbacks(loop); stopAdhan(); super.onDestroy(); }

              private void goForeground(String txt) {
                  String ch = "keepalive";
                  NotificationManager nm = (NotificationManager) getSystemService(NOTIFICATION_SERVICE);
                  Notification.Builder b;
                  if (Build.VERSION.SDK_INT >= 26) {
                      NotificationChannel c = new NotificationChannel(ch, "Adhan Alerts", NotificationManager.IMPORTANCE_LOW);
                      nm.createNotificationChannel(c);
                      b = new Notification.Builder(this, ch);
                  } else {
                      b = new Notification.Builder(this);
                  }
                  b.setContentTitle("ILMORA").setContentText(txt)
                   .setSmallIcon(android.R.drawable.ic_lock_idle_alarm).setOngoing(true);
                  startForeground(1, b.build());
              }

              private void announce(String prayer) {
                  try {
                      String ch = "adhan";
                      NotificationManager nm = (NotificationManager) getSystemService(NOTIFICATION_SERVICE);
                      Notification.Builder b;
                      if (Build.VERSION.SDK_INT >= 26) {
                          NotificationChannel c = new NotificationChannel(ch, "Prayer Announcements", NotificationManager.IMPORTANCE_HIGH);
                          nm.createNotificationChannel(c);
                          b = new Notification.Builder(this, ch);
                      } else {
                          b = new Notification.Builder(this);
                      }
                      Intent open = new Intent(this, MainActivity.class);
                      PendingIntent pi = PendingIntent.getActivity(this, 0, open,
                          Build.VERSION.SDK_INT >= 23 ? PendingIntent.FLAG_IMMUTABLE : 0);
                      b.setContentTitle("It's time for " + prayer).setContentText("Adhan is playing")
                       .setSmallIcon(android.R.drawable.ic_lock_idle_alarm).setAutoCancel(true).setContentIntent(pi);
                      nm.notify(2, b.build());
                  } catch (Exception e) {}
              }

              private void tick() {
                  try {
                      if (timingsJson != null) { try { timings = new JSONObject(timingsJson); } catch (Exception e) {} }

if (timings == null) { fetchTimings(); return; }
                      if (!prefs.getBoolean("adhanOn", true)) return;
                      Calendar cal = Calendar.getInstance();
                      String now = String.format(Locale.US, "%02d:%02d", cal.get(Calendar.HOUR_OF_DAY), cal.get(Calendar.MINUTE));
                      String[] order = {"Fajr", "Dhuhr", "Asr", "Maghrib", "Isha"};
                      for (String prayer : order) {
                          String t = timings.optString(prayer, "");
                          if (t.length() >= 5 && t.startsWith(now) && !fired.equals(prayer + now)) {
                              fired = prayer + now;
                              playAdhan();
                              announce(prayer);
                              break;
                          }
                      }
                  } catch (Exception e) {}
              }

              private void playAdhan() {
                  stopAdhan();
                  try {
                      mp = new MediaPlayer();
                      mp.setWakeMode(this, PowerManager.PARTIAL_WAKE_LOCK);
                      mp.setAudioStreamType(AudioManager.STREAM_MUSIC);
                      mp.setDataSource(ADHAN);
                      mp.setOnPreparedListener(new MediaPlayer.OnPreparedListener() {
                          public void onPrepared(MediaPlayer p) { p.start(); }
                      });
                      mp.setOnCompletionListener(new MediaPlayer.OnCompletionListener() {
                          public void onCompletion(MediaPlayer p) { stopAdhan(); }
                      });
                      mp.prepareAsync();
                  } catch (Exception e) {}
              }

              private void stopAdhan() {
                  try { if (mp != null) { mp.stop(); mp.release(); } } catch (Exception e) {}
                  mp = null;
              }

              private void fetchTimings() {
                  new Thread(new Runnable() {
                      public void run() {
                          try {
                              HttpURLConnection c = (HttpURLConnection) new URL("https://api.aladhan.com/v1/timings?method=1").openConnection();
                              c.setConnectTimeout(8000); c.setReadTimeout(8000);
                              BufferedReader r = new BufferedReader(new InputStreamReader(c.getInputStream(), StandardCharsets.UTF_8));
                              StringBuilder sb = new StringBuilder();
                              String line;
                              while ((line = r.readLine()) != null) sb.append(line);
                              r.close();
                              JSONObject j = new JSONObject(sb.toString());
                              timings = j.getJSONObject("data").getJSONObject("timings");
                          } catch (Exception e) {}
                      }
                  }).start();
              }
          }
          EOF
          cat > app/src/main/java/com/ilmora/app/BootReceiver.java <<'EOF'
          package com.ilmora.app;

          import android.content.BroadcastReceiver;
          import android.content.Context;
          import android.content.Intent;
          import android.os.Build;

          public class BootReceiver extends BroadcastReceiver {
              @Override
              public void onReceive(Context ctx, Intent i) {
                  if (Intent.ACTION_BOOT_COMPLETED.equals(i.getAction())) {
                      Intent svc = new Intent(ctx, AdhanService.class);
                      if (Build.VERSION.SDK_INT >= 26) ctx.startForegroundService(svc); else ctx.startService(svc);
                  }
              }
          }
          EOF

      - name: Build APK
        run: gradle assembleDebug --no-daemon

- name: Publish APK to GitHub Release
        env:
          GH_TOKEN: ${{ github.token }}
        run: |
          cp app/build/outputs/apk/debug/app-debug.apk ILMORA.apk
          gh release delete latest --yes --cleanup 2>/dev/null || true
          gh release create latest ILMORA.apk --title "ILMORA Native APK" --notes "FULL NATIVE Android app — Quran, Qibla compass, Azkar, Tasbeeh, background Adhan (works even when app is closed or phone restarts)."

      - uses: actions/upload-artifact@v4
        with:
          name: ILMORA-APK
          path: app/build/outputs/apk/debug/app-debug.apk
