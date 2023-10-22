# TicTakToeGame
Very basic android version of Tic Tac Toe game. I have made this app to understand the math behind TicTacToe game and how the user interacts with UI in android app code. This is my second app and first game app. I have taken help from GFG and CWH. 


This is the APP interface: ![image](https://github.com/meHypernova/TicTakToeGame/assets/146374681/3b7c90c3-f250-498a-9709-15102d49ae7b)

XML Code: 

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:scrollbarSize="20dp"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="30dp"
        android:layout_marginTop="50dp"
        android:layout_marginEnd="30dp"
        android:fontFamily="sans-serif"
        android:gravity="center"
        android:text="@string/apptitle"
        android:textSize="31sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <ImageView
        android:id="@+id/table"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:src="@drawable/tablenew"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textView" />

    <LinearLayout
        android:layout_width="290dp"
        android:layout_height="304dp"
        android:orientation="vertical"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textView">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:orientation="horizontal">

            <ImageView
                android:id="@+id/imageView1"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:onClick="tapping"
                android:padding="20sp"
                android:tag="0" />

            <ImageView
                android:id="@+id/imageView2"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:onClick="tapping"
                android:padding="20sp"
                android:tag="1" />

            <ImageView
                android:id="@+id/imageView3"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:onClick="tapping"
                android:padding="20sp"
                android:tag="2" />
        </LinearLayout>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:orientation="horizontal">

            <ImageView
                android:id="@+id/imageView4"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:onClick="tapping"
                android:padding="20sp"
                android:tag="3" />

            <ImageView
                android:id="@+id/imageView5"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:onClick="tapping"
                android:padding="20sp"
                android:tag="4" />

            <ImageView
                android:id="@+id/imageView6"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:onClick="tapping"
                android:padding="20sp"
                android:tag="5" />
        </LinearLayout>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:orientation="horizontal">

            <ImageView
                android:id="@+id/imageView7"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:onClick="tapping"
                android:padding="20sp"
                android:tag="6" />

            <ImageView
                android:id="@+id/imageView8"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:onClick="tapping"
                android:padding="20sp"
                android:tag="7" />

            <ImageView
                android:id="@+id/imageView9"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:onClick="tapping"
                android:padding="20sp"
                android:tag="8" />
        </LinearLayout>
    </LinearLayout>

    <TextView
        android:id="@+id/statusbar"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="30dp"
        android:text="@string/updatingtext"
        android:textSize="17dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent" />


</androidx.constraintlayout.widget.ConstraintLayout>




Main Activity Code

package com.example.tictaktoe;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.ImageView;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {


    /*

     These are assumptions that I have taken
     O==X
     1==0

     is 0 then X, if 1 then 0 if 2 the blank;

    */

    int activeplayer=0;
    int count=0;
    boolean gameactive=true;
    int []GameState={2,2,2,2,2,2,2,2,2}; //1D array showing starting state ie all are blank
    int[][] WinningState = {
            {0, 1, 2}, // Top row
            {3, 4, 5}, // Middle row
            {6, 7, 8}, // Bottom row
            {0, 3, 6}, // Left column
            {1, 4, 7}, // Middle column
            {2, 5, 8}, // Right column
            {0, 4, 8}, // Diagonal from top-left to bottom-right
            {2, 4, 6}  // Diagonal from top-right to bottom-left
    }; // total 8 possibilities

    public void tapping(View view){

        if(!gameactive){
            ResetGame(view);
        }

        ImageView img=(ImageView) view;
        int tappedImage=Integer.parseInt(img.getTag().toString());

        if(GameState[tappedImage]==2){
            /* all the actions will be performed only if GameState[tappedImage]
            * is having value 2 ie empty */
            count++;
            GameState[tappedImage]=activeplayer;
            img.setTranslationY(-1000f);

            if(activeplayer==0){
                img.setImageResource(R.drawable.crossnew); // placing the image to box
                activeplayer=1;
                TextView status=findViewById(R.id.statusbar);
                status.setText("0's Turn");
            }

            else{
                img.setImageResource(R.drawable.zeronew);
                activeplayer=0;
                TextView status=findViewById(R.id.statusbar);
                status.setText("X's Turn");
            }

            img.animate().translationYBy(1000f).setDuration(100);
        }

//        checking winner
        for(int[] WinningStateCheck:WinningState){

            /*int[] WinningStateCheck is an array, here for loop is range-based
            * int[] WinningStateCheck is taking each possible value of wining
            * condition and matching it with current GameSate index, it may or may
            * not be full, this will run each time we give an input
            *
            *
            *
            *
            * */
            if(GameState[WinningStateCheck[0]]==GameState[WinningStateCheck[1]]
                && GameState[WinningStateCheck[1]]==GameState[WinningStateCheck[2]]
            && GameState[WinningStateCheck[0]]!=2){

                /*GameState[WinningStateCheck[0]]!=2 bkz if three are empty the also
                2==2==2 but we are not considering it
                */

                    String winnerStr = null;
                    if(GameState[WinningStateCheck[0]]==0){

                    /*
                    WinningStateCheck[0]] this is the exact 1d array (e.g. {3, 4, 5})
                    wining condition as we are now inside if condition.
                    */

                    winnerStr="X is the Winner: Tap to Restart";
                    TextView status=findViewById(R.id.statusbar);
                    status.setText(winnerStr);
                    gameactive=false;

                    }

                else if(GameState[WinningStateCheck[0]]==1){
                    winnerStr="0 is the Winner: Tap to Restart";
                    TextView status=findViewById(R.id.statusbar);
                    status.setText(winnerStr);
                    gameactive=false;
                }

            }
        }

        if(count>=9){
            count=0;
            String winnerStr="Draw: No Winner Restarted...";
            TextView status=findViewById(R.id.statusbar);
            status.setText(winnerStr);

            ResetGame(view);
        }

    }

    private void ResetGame(View view) {
        gameactive=true;
        activeplayer=0;

        for(int i=0;i<GameState.length;i++){
            GameState[i]=2;
        }

        ((ImageView)findViewById(R.id.imageView1)).setImageResource(0); //0 means making it empty
        ((ImageView)findViewById(R.id.imageView2)).setImageResource(0);
        ((ImageView)findViewById(R.id.imageView3)).setImageResource(0);
        ((ImageView)findViewById(R.id.imageView4)).setImageResource(0);
        ((ImageView)findViewById(R.id.imageView5)).setImageResource(0);
        ((ImageView)findViewById(R.id.imageView6)).setImageResource(0);
        ((ImageView)findViewById(R.id.imageView7)).setImageResource(0);
        ((ImageView)findViewById(R.id.imageView8)).setImageResource(0);
        ((ImageView)findViewById(R.id.imageView9)).setImageResource(0);

    }

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
