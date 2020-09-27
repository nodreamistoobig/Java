package com.company;

import com.google.gson.Gson;
import com.google.gson.internal.bind.util.ISO8601Utils;
import org.json.JSONArray;
import org.json.JSONException;
import org.json.JSONObject;
import org.w3c.dom.ls.LSOutput;

import java.awt.*;
import java.io.*;

import java.net.URL;
import java.util.ArrayList;
import java.util.Collections;

class FullWeather {
    Coord coord;
    String base;
    MainInfo main;
    String name;
}

class Coord {
    double lot;
    double lat;
}

class MainInfo{
    double temp;
    double feels_like;
    double temp_min;
    double temp_max;
    int pressure;
    int humidity;
}

class City implements Comparable<City>{

    public City (int id, String name, double temp){
        this.id = id;
        this.name = name;
        this.temp = temp;
    }

    int id;
    double temp;
    String name;

    @Override
    public int compareTo(City c) {
        return Double.compare(temp, c.temp);
    }

    @Override
    public String toString(){
        return "\n name=" + name + " temp=" + temp;
    }
}

public class Main {
    static ArrayList<City> cities = new ArrayList<City>();

    public static int getTempByCity(int[] id) throws JSONException {
        Gson gson = new Gson();
        for (int i=0; i<id.length; i++) {
            String API_URL = "http://api.openweathermap.org/data/2.5/weather?id=" + id[i] + "&appid=1c84dd4b0b6f36ed27b70556b6ecb3b4&units=metric";
            try {
                URL url = new URL(API_URL);
                InputStream stream = (InputStream) url.getContent();
                InputStreamReader reader = new InputStreamReader(stream);
                FullWeather fullWeather = gson.fromJson(reader, FullWeather.class);
                City c = new City(i, fullWeather.name, fullWeather.main.temp);
                cities.add(c);
            } catch (IOException e) {
                System.out.println(e.getMessage());
            }
        }
        System.out.println(cities);
        Collections.sort(cities, Collections.reverseOrder());
        System.out.println(cities);
        return -1;
    }



    public static void main(String[] args) throws JSONException, FileNotFoundException {
        int id[] = new int[] {524901, 703448, 2643743, 1726701, 4016589, 4261361, 5128638, 6057856, 3429732, 6692263, 7536078};
        getTempByCity(id);
    }
}
