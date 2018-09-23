//Accessing google spreadsheet and JAVA
//Finding greatest temperature and Humidity
//operation in a day or throughout the year




import edu.duke.*;
import org.apache.commons.csv.*;
import java.io.*;
import java.util.*;
public class CsvMax
{
     public CSVRecord hottestHour(CSVParser parser)
     { 
         CSVRecord largestSoFar = null;
       
         for(CSVRecord currentRow:parser)
         {   
             if(largestSoFar==null)
             {
                 largestSoFar = currentRow;
             }
          else{
             
              double currentTemp = Double.parseDouble(currentRow.get("TemperatureF"));
              double largestTemp = Double.parseDouble(largestSoFar.get("TemperatureF"));
             
              if(currentTemp>largestTemp)
              {
                  largestSoFar = currentRow;
              }
            }
          
         
        }
     
        return largestSoFar;
    }
    public CSVRecord hotHumidity(CSVParser parser)
     { 
         CSVRecord largestSoFar = null;
       
         for(CSVRecord currentRow:parser)
         {   
             if(largestSoFar==null)
             {
                 largestSoFar = currentRow;
             }
          else{
             
              double currentTemp = Double.parseDouble(currentRow.get("Humidity"));
              double largestTemp = Double.parseDouble(largestSoFar.get("Humidity"));
             
              if(currentTemp>largestTemp)
              {
                  largestSoFar = currentRow;
              }
            }
          
         
        }
     
        return largestSoFar;
    }
   
    public void testHottestDay()//In Particular day
    {
        FileResource fr = new FileResource();
        CSVRecord largest = hottestHour(fr.getCSVParser());
        System.out.println("hOTTEST TEMPERATURE was"+largest.get("TemperatureF")+" at "+ largest.get("DateUTC"));
    }
    public CSVRecord hottestInManyDays()//In Number Of Days
    {
        CSVRecord largestSoFar = null;
        DirectoryResource dr = new DirectoryResource();//TO select Number of files we want to
        for(File f:dr.selectedFiles())
        {    
            FileResource fr = new FileResource(f);
            CSVRecord currentRow = hottestHour(fr.getCSVParser());
            if(largestSoFar==null)
            {
                largestSoFar = currentRow;
            }
            else
            { 
              double currentTemp = Double.parseDouble(currentRow.get("TemperatureF"));
              double largestTemp = Double.parseDouble(largestSoFar.get("TemperatureF"));
              if(currentTemp>largestTemp)
              {
                  largestSoFar = currentRow;
              }
            }
        }
         return largestSoFar;
    } 
     public CSVRecord greatestHumidity()//Humidity In Number Of Days
    {
        CSVRecord largestSoFar = null;
        DirectoryResource dr = new DirectoryResource();//TO select Number of files we want to
        for(File f:dr.selectedFiles())
        {    
            FileResource fr = new FileResource(f);
            CSVRecord currentRow = hotHumidity(fr.getCSVParser());
            if(largestSoFar==null)
            {
                largestSoFar = currentRow;
            }
            else
            { 
              double currentTemp = Double.parseDouble(currentRow.get("Humidity"));
              double largestTemp = Double.parseDouble(largestSoFar.get("Humidity"));
              if(currentTemp>largestTemp)
              {
                  largestSoFar = currentRow;
              }
            }
        }
         return largestSoFar;
    } 
    
    public void testHottestInManyDays()
    {
        CSVRecord largest = hottestInManyDays();
        System.out.println("HOTTEST tEMPERATURE is "+largest.get("TemperatureF")+" at "+largest.get("DateUTC"));
    }
     public void testHumidity()
    {
        CSVRecord largest = greatestHumidity();
        System.out.println("HOTTEST Humidity is "+largest.get("Humidity")+" at "+largest.get("DateUTC"));
    }
   
  }

                
