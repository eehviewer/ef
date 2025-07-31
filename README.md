def grade_exam(self, exam, answers):
        """
        评分整张试卷
        :param exam: 试卷对象
        :param answers: 用户答案字典 {question_id: answer}
        :return: 总分, 各题得分详情
        """
        total_score = 0
        details = []
        
        for q in exam['questions']:
            q_id = q['question_id']
            user_answer = answers get(q_id)
            question_score, comment = self grade_question(q, user_answer)
            
            details append({
                'question_id': q_id,
                'score': question_score,
                'comment': comment,
                'max_score': q['score']
            })
            
            total_score += question_score
        
        return round(total_score, 2), details
四、前端交互实现（React示例）
4 1 测试页面组件
jsx
import React, { useState, useEffect } from 'react';
import axios from 'axios';
 
const ExamPage = ({ examId, userId }) => {
    const [exam, setExam] = useState(null);
    const [questions, setQuestions] = useState([]);
    const [answers, setAnswers] = useState({});
    const [ti meLeft, setti meLeft] = useState(0);
    const [isSubmitted, setIsSubmitted] = useState(false);
    const [error, setError] = useState(null);
