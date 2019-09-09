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

/// @class GenericMap
/// A templated map that supports basic C types (& some custom types).
/// Underlying data is stored as raw byte blocks and reinterpreted as the desired type.
class GenericMap {
public:
  GenericMap() = default;

  /// store a value for a key
  template<typename T>
  void set(std::string key, T value) {
    uint8_t* data = new uint8_t[sizeof(T)];
    *reinterpret_cast<T*>(data) = value;
    params[key] = std::unique_ptr<uint8_t>(data);
  }

  /// retrieve a value for a key and provide a return value if the key is not found
  template<typename T>
  T get(std::string key, T default_value) {
    auto iter = params.find(key);
    return iter == params.end() ? default_value : *reinterpret_cast<T*>(iter->second.get());
  }

  template<> //std::string specialization
  void set(std::string key, std::string value) {
    uint8_t* data = new uint8_t[value.length() + 1];
    std::memcpy(data, value.c_str(), value.length());
    data[value.length()] = '\0';
    params[key] = std::unique_ptr<uint8_t>(data);
  }

  template<>  //std::string specialization
  std::string get(std::string key, std::string default_value) {
    auto iter = params.find(key);
    return iter == params.end() ? default_value : std::string((char*)iter->second.get());
  }

private:
  std::unordered_map<std::string, std::unique_ptr<uint8_t>> params;
};


int main() {
  GenericMap generic_map;
  generic_map.set<float>("gain", 0.5);
  generic_map.set<std::string>("name", "generic_map0");
  std::string query_key;

  query_key = "gain";
  std::cout << query_key+": " << generic_map.get<float>(query_key, -1) << std::endl;

  query_key = "name";
  std::string val = generic_map.get<std::string>(query_key, "not_found");
  std::cout << query_key+": " << generic_map.get<std::string>(query_key, "not_found") << std::endl;
}
```
