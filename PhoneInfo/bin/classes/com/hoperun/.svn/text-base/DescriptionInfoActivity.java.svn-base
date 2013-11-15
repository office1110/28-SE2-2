
package com.hoperun;

import java.io.File;
import java.io.InputStream;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.Iterator;
import java.util.List;
import java.util.zip.Inflater;

import android.app.Activity;
import android.app.ActivityManager;
import android.app.ActivityManager.MemoryInfo;
import android.app.ActivityManager.RunningServiceInfo;
import android.app.ActivityManager.RunningTaskInfo;
import android.content.Context;
import android.content.pm.ApplicationInfo;
import android.os.Bundle;
import android.telephony.TelephonyManager;
import android.util.DisplayMetrics;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.BaseAdapter;
import android.widget.ListView;
import android.widget.TextView;


public class DescriptionInfoActivity extends Activity 
{
	private TextView description = null;
	@Override
	public void onCreate(Bundle savedInstanceState)
	{
		 super.onCreate(savedInstanceState);
	     setContentView(R.layout.description_info);
	     
	     description = (TextView)findViewById(R.id.description);
	     
	     String desName = getIntent().getStringExtra("desName");
	     
	     String[] cmdArgs = new String[]{"/system/bin/cat","/proc/version"};
	     
	     if(desName.equals("操作系统信息"))
	     {
	    	 description.setText(cmdExcute(cmdArgs,"/system/bin/"));
	     }
	     else if(desName.equals("系统信息"))
	     {
	    	 StringBuffer sb = new StringBuffer();
	    	 sb.append("java.vendor.url：");
	    	 sb.append(System.getProperty("java.vendor.url"));
	    	 sb.append("\n");
	    	 
	    	 sb.append("file.encoding:");
	    	 sb.append(System.getProperty("file.encoding"));
	    	 sb.append("\n");
	    	 
	    	 sb.append("java.home:");
	    	 sb.append(System.getProperty("java.home"));
	    	 description.setText(sb.toString());
	     }
	     else if(desName.equals("运营商信息"))
	     {
	    	 TelephonyManager tm = (TelephonyManager)getSystemService(Context.TELEPHONY_SERVICE);
	    	 String rst = "PhoneType:"+tm.getPhoneType();
	    	 description.setText(rst);
	     }
	     else if(desName.equals("cpu信息"))
	     {
	    	 cmdArgs = new String[]{"/system/bin/cat","/proc/cpuinfo"};
	    	 description.setText(cmdExcute(cmdArgs,"/system/bin/"));
	     }
	     else if(desName.equals("内存信息"))
	     {
//	    	 cmdArgs = new String[]{"/system/bin/cat","/proc/meminfo"};
//	    	 description.setText(cmdExcute(cmdArgs,"/system/bin/"));
	    	 ActivityManager am = (ActivityManager)getSystemService(Context.ACTIVITY_SERVICE);
	    	 MemoryInfo mi = new ActivityManager.MemoryInfo();
	    	 description.setText("memory："+mi.availMem);
	     }
	     else if(desName.equals("网络信息"))
	     {
	    	 cmdArgs = new String[]{"/system/bin/netcfg"};
	    	 description.setText(cmdExcute(cmdArgs,"/system/bin/"));
	     }
	     else if(desName.equals("硬盘信息"))
	     {
	    	 cmdArgs = new String[]{"/system/bin/df"};
	    	 description.setText(cmdExcute(cmdArgs,"/system/bin/"));
	     }
	     else if(desName.equals("显示屏信息"))
	     {
	    	DisplayMetrics dm = this.getResources().getDisplayMetrics();
	    	int screenWidth = dm.widthPixels;
	    	int screenHeight = dm.heightPixels;
	    	
	    	float density = dm.density;
	    	float xdpi = dm.xdpi;
	    	float ydpi = dm.ydpi;
	    	
	    	String rst = "绝对宽："+screenWidth+"\n 绝对高："+screenHeight+"\n 分辨率："+density+"\n X:"+xdpi+"\n Y："+ydpi;
	    	description.setText(rst);
	     }
	     else if(desName.equals("软件信息"))
	     {
	    	//List<HashMap<String,Object>> appListInfo = new ArrayList<HashMap<String,Object>>();
	    	final List<ApplicationInfo> appListInfo = getPackageManager().getInstalledApplications(0);
	    	ListView appList = (ListView)findViewById(R.id.softinfo);
	    	appList.setAdapter(new BaseAdapter() {
				
				public View getView(int position, View convertView, ViewGroup parent) 
				{
					LayoutInflater inflat = getLayoutInflater();
					View view = inflat.inflate(android.R.layout.simple_list_item_2, null);
					TextView tv1= (TextView)view.findViewById(android.R.id.text1);					
					TextView tv2= (TextView)view.findViewById(android.R.id.text2);
					ApplicationInfo appinfo = appListInfo.get(position);
					String appName = getPackageManager().getApplicationLabel(appinfo).toString();
					tv1.setText(appName);
					tv2.setText(appinfo.packageName);
					return view;
				}
				
				public long getItemId(int position) 
				{
					return position;
				}
				
				public Object getItem(int position) 
				{
					return appListInfo.get(position);
				}
				
				public int getCount() 
				{
					return appListInfo.size();
				}
			});
	     }
	     else if(desName.equals("运行的服务"))
		 {
	    	 StringBuffer sb=new StringBuffer();
	    	 ActivityManager am=(ActivityManager) getSystemService(ACTIVITY_SERVICE);
	    	 List listser=am.getRunningServices(100);
	    	 for(int i=0;i<listser.size();i++){
	    		 RunningServiceInfo curser=(RunningServiceInfo) listser.get(i);
	    		 String rst=curser.pid+curser.process+curser.activeSince+"";
	    		 description.setText(rst);
	    	 }
		 }
	     else if(desName.equals("运行的任务"))
		 {
	    	 StringBuffer sb = new StringBuffer();
	    	 ActivityManager am = (ActivityManager)getSystemService(Context.ACTIVITY_SERVICE);
	    	 List<RunningTaskInfo> listTask  = am.getRunningTasks(100);
	    	 for(int i=0;i<listTask.size();i++)
	    	 {
	    		 RunningTaskInfo curSer = listTask.get(i);
	    		 sb.append("baseActivity:"+curSer.baseActivity+"\n");
	    		 sb.append("numActivity:"+curSer.numActivities+"\n");
	    		 sb.append("numRunning:"+curSer.numRunning+"\n");
	    		 sb.append("desctiption:"+curSer.description+"\n");
	    	 }
	    	 description.setText(sb.toString());
		 }
	     else if(desName.equals("运行的进程"))
		 {
	    	 cmdArgs = new String[]{"/system/bin/top","-n","1"};
	    	 description.setText(cmdExcute(cmdArgs,"/system/bin/"));
		 }
	     
	}
	
	public String cmdExcute(String args[],String workDirectory)
	{
		String rst = "";
		try
		{
		
		ProcessBuilder buider = new ProcessBuilder(args);
		buider.directory(new File(workDirectory));
		
		buider.redirectErrorStream(true);
		
		Process process = buider.start();
		InputStream is = process.getInputStream();
		byte[] bytes = new byte[1024];
		while(is.read(bytes)!=-1)
		{
			rst += new String(bytes);
		}
		
		}
		catch(Exception ce)
		{
			ce.printStackTrace();
		}
		return rst;
	}
}
