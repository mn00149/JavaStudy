```
package com.cos.security1.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class IndexController {

	@GetMapping("/")
	public String index() {
		//머스테치 기본 폴더 src/main/resources/
		//뷰리졸버설정 생략가능
		return "index";
	}
	
	@GetMapping("/user")
	public String user() {
	
		return "user";
	}
	
	@GetMapping("/manager")
	public String manager() {
	
		return "manager";
	}
	
	@GetMapping("/admin")
	public String admin() {
	
		return "admin";
	}
	
	//스프링 시큐리티가 낚아챔
	@GetMapping("/login")
	public String login() {
	
		return "login";
	}
	
	@GetMapping("/join")
	public String join() {
	
		return "join";
	}
	
	@GetMapping("/joinProc")
	public @ResponseBody String joinProc() {
	
		return "회원가입 완료";
	}
	
	
}
```