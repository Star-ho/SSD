---
date: 2024-04-21 15:02:55+0000
updatedAt: 2024-04-21 15:44:53+0590
tags: 
---
package team.hlab.infrastructure.jpa

import org.springframework.boot.autoconfigure.EnableAutoConfiguration
import org.springframework.boot.test.autoconfigure.jdbc.AutoConfigureTestDatabase
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest
import org.springframework.context.annotation.ComponentScan
import org.springframework.data.jpa.repository.config.EnableJpaAuditing
import org.springframework.test.context.ActiveProfiles
import org.springframework.test.context.ContextConfiguration

@ComponentScan
@EnableJpaAuditing
@EnableAutoConfiguration
private class SpringJpaTestConfiguration

@ActiveProfiles("local")
@ContextConfiguration(classes = [SpringJpaTestConfiguration::class])
@AutoConfigureTestDatabase(replace = AutoConfigureTestDatabase.Replace.NONE)
@DataJpaTest
annotation class SpringJpaTest

#Test  