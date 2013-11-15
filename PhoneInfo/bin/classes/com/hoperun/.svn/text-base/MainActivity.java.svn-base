package com.hoperun;

import java.util.List;

import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.AdapterView.OnItemClickListener;
import android.widget.ArrayAdapter;
import android.widget.ListView;

public class MainActivity extends Activity {
	
	private ListView indexListView = null;
	
	String[] indexInfo = new String[]
	                                {
										"系统信息",
										"硬件信息",
										"软件信息",
										"运行时信息"
	                                };
    @Override
    public void onCreate(Bundle savedInstanceState) 
    {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
        
        indexListView = (ListView)findViewById(R.id.index_listview);
        
        indexListView.setAdapter(new ArrayAdapter<String>(
        								this, 
        								android.R.layout.simple_list_item_1,
        								android.R.id.text1,
        								indexInfo
        								));
        indexListView.setOnItemClickListener(new OnItemClickListener() 
        {

			public void onItemClick(AdapterView<?> parent, View view,
					int position, long id) 
			{
				Intent intent = new Intent(MainActivity.this,SecondInfoActivity.class);
				intent.putExtra("itemName", indexInfo[position]);
				startActivity(intent);
			}
		});
        
    }
}