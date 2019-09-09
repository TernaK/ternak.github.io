## GenericMap

### build
```
g++ -std=c++11 -o generic_map generic_map.cpp
```

### generic_map.cpp
```c++
#include <iostream>
#include <unordered_map>
#include <memory>

class GenericMap {
public:
  GenericMap() = default;

  template<typename T>
  void set_generic(std::string key, T value) {
    uint8_t* data = new uint8_t[sizeof(T)];
    *((T*)data) = value;
    params.insert({ key, std::unique_ptr<uint8_t>(data) });
  }

  template<typename T>
  T get_generic(std::string key, T default_value) {
    auto iter = params.find(key);
    return iter == params.end() ? default_value : *((T*)iter->second.get());
  }

  void set_bool(std::string key, bool value) { set_generic<bool>(key, value); }
  void set_float(std::string key, float value) { set_generic<float>(key, value); }
  void set_int(std::string key, int value) { set_generic<int>(key, value); }
  bool get_bool(std::string key, float default_value) { return get_generic<bool>(key, default_value); }
  float get_float(std::string key, float default_value) { return get_generic<float>(key, default_value); }
  int get_int(std::string key, float default_value) { return get_generic<int>(key, default_value); }

  void set_string(std::string key, std::string value) {
    uint8_t* data = new uint8_t[value.length() + 1];
    std::memcpy(data, value.c_str(), value.length());
    data[value.length()] = '\0';
    params.insert({ key, std::unique_ptr<uint8_t>(data) });
  }

  std::string get_string(std::string key, std::string default_value) {
    auto iter = params.find(key);
    return iter == params.end() ? default_value : std::string((char*)iter->second.get());
  }

private:
  std::unordered_map<std::string, std::unique_ptr<uint8_t>> params;
};


int main() {
  GenericMap generic_map;
  generic_map.set_float("gain", 0.5);
  generic_map.set_string("name", "generic_map");

  std::string query_key = "gain";
  std::cout << query_key+": " << generic_map.get_float(query_key, -1) << std::endl;

  query_key = "name";
  std::cout << query_key+": " << generic_map.get_string(query_key, "not_found") << std::endl;
}
```
