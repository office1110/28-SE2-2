
package com.hoperun;

import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.AdapterView.OnItemClickListener;
import android.widget.ArrayAdapter;
import android.widget.ListView;


public class SecondInfoActivity extends Activity 
{
	private ListView secondListView = null;
	private String[] tempList = null;
	String[][] secondPageIndex = new String[][]
	                                          {
												{"操作系统信息","系统信息","运营商信息"},
												{"cpu信息","内存信息","网络信息","硬盘信息","显示屏信息"},
												{"运行的服务","运行的任务","运行的进程"}
	                                          };
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		 	super.onCreate(savedInstanceState);
	        setContentView(R.layout.secondpage);
	        
	        String itemName = getIntent().getExtras().get("itemName").toString();
	        setTitle(itemName);
	        secondListView = (ListView)findViewById(R.id.second_listview);
	        
	      
	        
	        if(itemName.equals("系统信息"))
	        {
	        	tempList = secondPageIndex[0];
	        }
	        else if(itemName.equals("硬件信息"))
	        {
	        	tempList = secondPageIndex[1];
	        }
	        else if(itemName.equals("软件信息"))
	        {
	        	Intent intent = new Intent(SecondInfoActivity.this,DescriptionInfoActivity.class);
	        	intent.putExtra("desName", "软件信息");
	        	startActivity(intent);
	        }
	        else if(itemName.equals("运行时信息"))
	        {
	        	tempList = secondPageIndex[2];
	        }
	        if(tempList!=null)
	        {
	        	secondListView.setAdapter(new ArrayAdapter<String>(
	        														this, 
	        														android.R.layout.simple_list_item_1,
	        														android.R.id.text1,
	        														tempList));
	        }
	        
	        
	        secondListView.setOnItemClickListener(new OnItemClickListener() 
	        {

				public void onItemClick(AdapterView<?> parent, View view,
						int position, long id) 
				{
					Intent intent = new Intent(SecondInfoActivity.this,DescriptionInfoActivity.class);
		        	intent.putExtra("desName", tempList[position]);
		        	startActivity(intent);
				}
			});
	        
	        
	}
}
